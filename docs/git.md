# git + lazygit

## git (`git/.gitconfig`)

- **Identity**: name, email, and GPG signing key ID (`user.signingkey` is the
  public key ID — the private key lives in `~/.gnupg` and moves between
  machines manually, never through this repo)
- **Signing**: `commit.gpgsign = true` — every commit is signed. A machine
  without the private key imported will refuse to commit; that's the signal to
  run `gpg --import` there
- **Pager**: delta everywhere — `core.pager` for diff/log/show,
  `interactive.diffFilter` for `git add -p`. `navigate = true` (n/N jump
  between files), `side-by-side = true` (falls back to unified in narrow
  terminals — that's width detection, not breakage)
- **Merge**: `conflictstyle = diff3` shows the common ancestor in conflicts
- **Credentials**: `gh auth git-credential` handles github.com; nothing
  credential-shaped is stored in this repo

## lazygit (`config/lazygit/config.yml`)

One job: render diffs through delta (`diffRenderers`, needs lazygit >= 0.62),
same dark theme and line numbers as the git pager, plus `lazygit-edit://`
hyperlinks so file:line references are clickable in Ghostty.

macOS lazygit reads `~/Library/Application Support/lazygit/config.yml`, which
is symlinked to the same file — see the link map in the README. Launched via
the `lg` alias or from nvim's lazygit plugin.
