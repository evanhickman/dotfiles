# dotfiles

Managed with [chezmoi](https://chezmoi.io). zsh + Oh My Zsh, starship prompt,
git, vim, VS Code, and a Brewfile that installs everything.

## New machine setup

1. Install [Homebrew](https://brew.sh)
2. `brew install chezmoi`
3. `chezmoi init --apply evanhickman`

Step 3 prompts for a git email address and a machine profile (`work` or
`personal`), then writes both to `~/.config/chezmoi/chezmoi.toml`. That file
stays local and never enters this public repo.

`run_onchange_install-packages.sh` installs every Homebrew package, cask, and
VS Code extension from `.Brewfile` on first apply, and re-runs whenever the
Brewfile changes.

## Daily use

    chezmoi edit <file>   # edit source
    chezmoi diff          # preview
    chezmoi apply         # write to home
    chezmoi cd            # git add/commit/push from here

## Profiles

`profile` selects the config a machine gets. `chezmoi init` prompts for it and
stores it in the local config; `.chezmoi.toml.tmpl` defines that prompt and
defaults it to `personal`.

Templates read `.profile` directly, so a hand-written config that omits it fails
loudly rather than applying personal config to a work machine.

chezmoi applies these only when `profile = "work"`:

- Zscaler CA exports in `.zshrc`, and `http.sslCAInfo` in `.gitconfig`
- `mkt` and `aiss` navigation aliases

Templating controls what gets *applied*, not what is *visible*. This repo is
public, so anything that must stay unreadable lives outside it rather than
behind a profile guard. Claude Code's agent definitions in `~/.claude/agents`
are tracked here and contain no personal information. The global
`~/.claude/CLAUDE.md` is not tracked, because it names an employer and internal
repos. IT provisions the Zscaler `.pem` files; this repo does not track them
either.
