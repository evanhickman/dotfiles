# dotfiles

Managed with [chezmoi](https://chezmoi.io). zsh + Oh My Zsh, starship prompt,
git, vim, VS Code, and a Brewfile that installs everything.

## New machine setup

1. Install [Homebrew](https://brew.sh)
2. `brew install chezmoi`
3. Recreate the local config (holds values kept out of this public repo):

       mkdir -p ~/.config/chezmoi
       cat > ~/.config/chezmoi/chezmoi.toml <<'EOF'
       [data]
           email = "<git email>"
       EOF

4. `chezmoi init --apply evanhickman`

The `run_once_install-packages.sh` script runs automatically on first apply
and installs all Homebrew packages, casks, and VS Code extensions from
`.Brewfile`.

## Daily use

    chezmoi edit <file>   # edit source
    chezmoi diff          # preview
    chezmoi apply         # write to home
    chezmoi cd            # git add/commit/push from here
