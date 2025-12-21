# Ansible Role: vim

An Ansible role to install and configure Vim with a curated set of plugins and a custom configuration tailored for development workflows.

## Description

This role automates the installation of Vim and sets up a personalized development environment with popular plugins including Gruvbox theme, vim-airline, and vim-fugitive. It deploys a custom `.vimrc` configuration optimized for coding with features like syntax highlighting, smart indentation, and visual indicators for whitespace.

## Requirements

- Ansible 2.20 or higher
- Git (automatically installed by the role)
- Supported operating systems:
  - Debian (bookworm, buster, bullseye)
  - macOS (via Homebrew)

## Role Variables

Available variables are listed below, along with default values (see [defaults/main.yml](defaults/main.yml)):

```yaml
vim_users:
  - hferreira
  - root
```

List of users for whom Vim will be configured. The role will set up the Vim environment for each user specified.

```yaml
vim_dir: "$HOME/.vim/pack/default/start/"
```

Directory where Vim plugins will be installed using Vim 8's native package management.

```yaml
vim_git_repos:
  - name: "vim-fugitive"
    repo: 'https://github.com/tpope/vim-fugitive.git'
    dest: "{{ vim_dir }}/fugitive"
    version: "master"

  - name: "gruvbox"
    repo: 'https://github.com/morhetz/gruvbox.git'
    dest: "{{ vim_dir }}/gruvbox"
    version: "master"

  - name: "vim-airline"
    repo: 'https://github.com/vim-airline/vim-airline.git'
    dest: "{{ vim_dir }}/vim-airline"
    version: "master"

  - name: "vim-airline-themes"
    repo: 'https://github.com/vim-airline/vim-airline-themes.git'
    dest: "{{ vim_dir }}/vim-airline-themes"
    version: "master"

  - name: "vim-bracketed-paste"
    repo: 'https://github.com/ConradIrwin/vim-bracketed-paste.git'
    dest: "{{ vim_dir }}/vim-bracketed-paste"
    version: "master"
```

List of Vim plugins to install. Each plugin is cloned from its Git repository.

## Installed Plugins

- **vim-fugitive**: Git wrapper for Vim
- **gruvbox**: Retro groove color scheme
- **vim-airline**: Lean & mean status/tabline
- **vim-airline-themes**: Theme repository for vim-airline
- **vim-bracketed-paste**: Automatic paste mode

## Vim Configuration Features

The deployed [`.vimrc`](files/vimrc) includes:

- Gruvbox dark theme with hard contrast
- Powerline fonts support for vim-airline
- Syntax highlighting enabled
- Smart indentation (2 spaces)
- Line numbers enabled
- Automatic removal of trailing whitespace on save
- Invisible character indicators (spaces, tabs, EOL)
- No swap files or backup files
- 256 color support
- Alacritty terminal compatibility

## Dependencies

None.

## Example Playbook

```yaml
- hosts: workstations
  roles:
    - hferreira23.vim
```

With custom user list:

```yaml
- hosts: workstations
  roles:
    - role: hferreira23.vim
      vim_users:
        - developer
        - admin
```

With custom plugins:

```yaml
- hosts: workstations
  roles:
    - role: hferreira23.vim
      vim_git_repos:
        - name: "nerdtree"
          repo: 'https://github.com/preservim/nerdtree.git'
          dest: "{{ vim_dir }}/nerdtree"
          version: "master"
```

## Testing

This role includes automated testing via GitHub Actions:

- **Ansible Lint**: Validates role syntax and best practices
- **Commit Lint**: Ensures commit messages follow conventional commits
- **Semantic Versioning**: Automatic version bumping and releases

## License

MIT

## Author Information

Created by Hugo Ferreira.

- Galaxy: [hferreira23.vim](https://galaxy.ansible.com/hferreira23/vim)
- GitHub: [hferreira23/vim](https://github.com/hferreira23/vim)
