This is my current development setup.

# On Windows
## Install Windows Subsystem for Linux (WSL)

Enable WSL in developer options and then install Ubuntu from the Microsoft Store.

From the Ubuntu app, install **curl**:
```
sudo apt-get install curl
```
and **git**:
```
sudo apt-add-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```
and **zsh**:
```
sudo apt-get install zsh
```
and **oh-my-zsh**
```
curl -L https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh | bash
```
To make zsh run by default (over bash), edit `.bashrc` with `vim ~./bashrc` (don't use Windows apps to edit linux files) and add to the top:
```
bash -c zsh
```

## Install Hyperterm(inal)
Download and install [hyperterm](https://hyper.is/). To use the Linux shell, open preferences (from app menu or `%USERPROFILE%/.hyper.js`) and edit:
```
shell: 'C:\\Windows\\System32\\bash.exe',
shellArgs: ['--login', '-i', '/c wsl'],
```
### Customize Hyperterm with plugins
Edit hyperterm preferences with:
```
config: {
  hyperBorder: {
    borderWidth : "1px",
    animate: {duration : "1s"},
  }
}

plugins: [
  "hyperborder",
  "hyperterm-cursor",
  "gitrocket",
  "hyperterm-summon",
  "hyper-solarized-light"
],

```
- hyperborder: adds an animated color border
- hyperterm-cursor: inverts font color under block cursor
- gitrocket: fun animated rocket at `git push`
- hyperterm-summon: hide and show hyperterm with `[ctrl][;]`
- hyper-solarized-light: color scheme

## Customize zsh
### Plugins
*Note: I have been unable to use a plugin manager due to carriage return errors.*

[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting): highlights command syntax. Helps catch typos. Download with:
```
 git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions): suggests commands while typing. Accept with [→]. Download with:
```
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```
[z](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/z): jump to frequently visited directories by keyword. For example, `z blo` can select `~/dev/projects/personal-blog/`. Download z.sh from [its GitHub repo](https://github.com/rupa/z) and add to your home directory.

Enable these plugins by editing the `.zshrc` file in your home directory. Open with `vim ~.zshrc` and edit:
```
plugins=(
  git
  z
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```

### Theme
[Powerlevel9k](https://github.com/bhilburn/powerlevel9k) is a customizable theme for zsh. First, you will need to install a [powerline font](https://github.com/powerline/fonts). I'm using a [patched nerd-font](https://github.com/ryanoasis/nerd-fonts), Inconsolata NF, which offers extra glyphs. Simply download the font file (.tff) and right click to install.

Change the font in hyper preferences. In addition, edit the following line to fix powerline alignment:
```
termCSS: 'x-row {line-height: initial} .unicode-node {position: relative}',
```
Download Powerlevel9k with:
```
$ git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```
To enable the theme, edit `~./zshrc`:
```
ZSH_THEME="powerlevel9k/powerlevel9k"
```
I slightly stripped down my configuration of the theme. My `~.zshrc` looks like:
```
POWERLEVEL9K_MODE='nerdfont-complete'
ZSH_THEME="powerlevel9k/powerlevel9k"

POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir rbenv vcs)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status background_jobs time os_icon)
POWERLEVEL9K_LEFT_SEGMENT_SEPARATOR=''
POWERLEVEL9K_RIGHT_SEGMENT_SEPARATOR=''
POWERLEVEL9K_LEFT_SUBSEGMENT_SEPARATOR='|'
POWERLEVEL9K_RIGHT_SUBSEGMENT_SEPARATOR='|'
POWERLEVEL9K_DIR_HOME_BACKGROUND="clear"
POWERLEVEL9K_DIR_HOME_FOREGROUND="blue"
POWERLEVEL9K_DIR_HOME_SUBFOLDER_BACKGROUND="clear"
POWERLEVEL9K_DIR_HOME_SUBFOLDER_FOREGROUND="blue"
POWERLEVEL9K_DIR_DEFAULT_BACKGROUND="clear"
POWERLEVEL9K_DIR_DEFAULT_FOREGROUND="blue"
POWERLEVEL9K_VCS_MODIFIED_BACKGROUND="clear"
POWERLEVEL9K_VCS_UNTRACKED_BACKGROUND="clear"
POWERLEVEL9K_VCS_MODIFIED_FOREGROUND="yellow"
POWERLEVEL9K_VCS_UNTRACKED_FOREGROUND="yellow"
POWERLEVEL9K_STATUS_OK_BACKGROUND="clear"
POWERLEVEL9K_STATUS_OK_FOREGROUND="green"
POWERLEVEL9K_STATUS_ERROR_BACKGROUND="clear"
POWERLEVEL9K_STATUS_ERROR_FOREGROUND="red"
POWERLEVEL9K_TIME_BACKGROUND="clear"
POWERLEVEL9K_TIME_FOREGROUND="white"

POWERLEVEL9K_PROMPT_ON_NEWLINE=true
POWERLEVEL9K_PROMPT_ADD_NEWLINE=true
POWERLEVEL9K_SHORTEN_DIR_LENGTH=3
POWERLEVEL9K_SHORTEN_DELIMITER=".."
POWERLEVEL9K_SHORTEN_STRATEGY=None
```
*NOTE: the line `POWERLEVEL9K_MODE=''` must come before the theme selection. Exclude this  if you are using a powerline font. Use `POWERLEVEL9K_MODE='awesome-patched'` for patched awesome-powerline fonts. I have `POWERLEVEL9K_MODE='nerdfont-complete'` because I am using a nerd-font.*

### VIM
