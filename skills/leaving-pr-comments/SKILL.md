---
name: leaving-pr-comments
description: Mark every GitHub comment posted on Andreas's behalf as AI-written, and format and post it correctly. Use whenever leaving or replying to PR comments (top-level, inline, review summaries, or review threads), responding to reviewer or bot feedback, or posting via `gh pr comment`, `gh pr review`, or the GitHub API — including when /code-review is run with --comment.
---

# Leaving PR comments

Anything posted to GitHub is public to everyone on the repo, so every comment
you write must say plainly that an AI wrote it, not Andreas.

## The AI marker

Start every comment you post with this GitHub note callout:

```md
> [!NOTE]
> 🤖 **<model> commenting on behalf of Andreas (@furst)**

The comment itself starts here.
```

- `<model>` is your verified public model name, e.g. `Claude Opus 5.5`. If you
  don't know it for sure, use the harness name (`Claude Code`, `Codex`). Don't
  guess a version.
- Use `responding` instead of `commenting` when replying to someone else's
  comment.
- The note holds only the attribution. The comment body goes after a blank
  line, outside the callout.
- Add one marker per comment. Don't add a signature footer, a horizontal rule,
  or a second attribution.
- Every inline review comment gets its own marker, because GitHub shows inline
  comments on their own in the Files view.

The marker goes on top-level PR comments, review summaries, inline comments,
thread replies, and explanations posted before resolving or dismissing
feedback. Leave it off PR descriptions, commit messages, and text Andreas asks
you to post verbatim without it.

## Writing the comment

- Lead with the conclusion.
- Point to the specific code, test, check, or repro.
- Say what's verified and what's judgment.
- Write in plain sentences, the way a person would. Don't structure the
  comment as `key: value` labels like `**Issue:** … **Impact:** … **Fix:** …`.
- Keep it short. No filler, canned thanks, or narrating what you did.
- Check the whole comment, including quoted text, for secrets, internal URLs,
  or private details before you post it.

## Posting

Top-level comment:

```sh
gh pr comment <n> --body-file comment.md
```

Review with inline comments, all in one submission so the PR author gets a
single notification:

```sh
gh api repos/{owner}/{repo}/pulls/<n>/reviews -X POST --input review.json
```

```json
{
  "event": "COMMENT",
  "body": "> [!NOTE]\n> 🤖 **Claude Opus 5.5 commenting on behalf of Andreas (@furst)**\n\nSummary…",
  "comments": [
    {
      "path": "src/foo.ts",
      "line": 42,
      "side": "RIGHT",
      "body": "> [!NOTE]\n> 🤖 **Claude Opus 5.5 commenting on behalf of Andreas (@furst)**\n\nThis throws when…"
    }
  ]
}
```

Reply to an existing review thread:

```sh
gh api repos/{owner}/{repo}/pulls/<n>/comments/<comment_id>/replies -X POST -F body=@reply.md
```

Write bodies to a file rather than passing them inline. Shell quoting breaks
the `>` lines and the blank line after the callout.

After posting, confirm GitHub returned the comment or review URL and pass it
on to Andreas. Resolve a thread only after your reply was posted
successfully.
