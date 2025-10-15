# p6m7g8-actions/p6-gh-pr-auto-enqueue

- [p6m7g8-actions/p6-gh-pr-auto-enqueue](#p6m7g8-actionsp6-gh-pr-auto-enqueue)
  - [Usage](#usage)

## Usage

```yaml
      - name: Enqueue PR to GH Merge Queue
        uses: p6m7g8-actions/p6-gh-pr-auto-enqueue@main
        with:
          gh_token: ${{ secrets.GITHUB_TOKEN }}
```