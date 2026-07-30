# p6m7g8-actions/p6-gh-pr-auto-enqueue

- [p6m7g8-actions/p6-gh-pr-auto-enqueue](#p6m7g8-actionsp6-gh-pr-auto-enqueue)
  - [Usage](#usage)
  - [Outcomes](#outcomes)

## Usage

```yaml
      - name: Enqueue PR to GH Merge Queue
        uses: p6m7g8-actions/p6-gh-pr-auto-enqueue@main
        with:
          gh_token: ${{ secrets.GITHUB_TOKEN }}
```

## Outcomes

The enqueue step classifies the `enqueuePullRequest` result and prints one
`RESULT:` line so the run output states plainly what happened.

| Outcome    | When                                                             | Exit |
|------------|------------------------------------------------------------------|------|
| `enqueued` | The mutation succeeded and the PR is in the merge queue          | 0    |
| `skipped`  | The PR is already queued, already merged, or no longer open      | 0    |
| `retried`  | A required status or approval had not settled; retried in-run    | 0/1  |
| `failed`   | No merge queue configured on the base branch, or any other error | 1    |

Benign outcomes are deliberately narrow. This action fires exactly once per
`Build` `workflow_run` completion and there is no retry trigger, so swallowing
every failure would silently strand a PR outside the queue. Transient gates get
at most three attempts with bounded in-run backoff, then fail red so the signal
survives. A repository with no merge queue rule fails with an actionable message
naming the repository rather than a raw GraphQL dump.
