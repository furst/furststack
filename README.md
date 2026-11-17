# furststack

The agent skills I use, kept in one place. They work in Claude Code and Codex.
Inspired by [tstack](https://github.com/t3dotgg/tstack).

## Skills

| Skill                 | Say         | What it does                                                                                  |
| --------------------- | ----------- | --------------------------------------------------------------------------------------------- |
| `leaving-pr-comments` | (automatic) | Marks every comment an agent posts on your behalf as AI-written, and keeps it in plain prose. |

## Install

```bash
git clone https://github.com/furst/furststack
cp -R furststack/skills/* ~/.claude/skills/   # Claude Code
cp -R furststack/skills/* ~/.codex/skills/    # Codex
```

To keep a single copy, symlink each skill instead of copying it:

```bash
ln -s "$PWD/furststack/skills/leaving-pr-comments" ~/.claude/skills/leaving-pr-comments
```

## Requirements

- An authenticated [GitHub CLI](https://cli.github.com) (`gh`).

## Make them yours

`leaving-pr-comments` names me (Andreas, @furst) in its attribution line.
Swap in your own name and GitHub login before you use it.

## License

[MIT](LICENSE)
