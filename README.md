```
       d8888 888 888
      d88888 888 888
     d88P888 888 888
    d88P 888 888 888888 888  888 888  888
   d88P  888 888 888    888  888 `Y8bd8P'    +--------------+
  d88P   888 888 888    888  888   X88K     /  Alt         /
 d8888888888 888 Y88b.  Y88b 888 .d8""8b.  /         tux  /
d88P     888 888  "Y888  "Y88888 888  888 +--------------+
```

---

# Altux

Hold the Alt key as your tmux prefix

Press `Alt+c` to create a window, `Alt+d` to detach. `Alt+%` to split, etc. All
other native tmux keybindings are alsso ssupported 

## Install

### Manual

```sh
mkdir -p ~/.config/tmux
curl -fLo ~/.config/tmux/altux.conf https://raw.githubusercontent.com/eduardofuncao/altux/main/altux.conf
```

Then in your `tmux.conf`:

```
source-file ~/.config/tmux/altux.conf
```

### TPM

Add to your `tmux.conf`:

```
set -g @plugin 'eduardofuncao/altux'
```

Press `prefix + I` to install.

### NixOS

```nix
programs.tmux = {
  enable = true;
  plugins = [
    {
      plugin = pkgs.tmuxPlugins.mkTmuxPlugin {
        pluginName = "altux";
        version = "0.1.0-beta";
        src = pkgs.fetchFromGitHub {
          owner = "eduardofuncao";
          repo = "altux";
          rev = "main";
          hash = "";  # first build fails, replace with correct hash
        };
      };
    }
  ];
};
```

## Bindings

All bindings use the root table (`bind -n`). These do not interefere with your set prefix.

### Panes

| Key | Action | Default |
|-----|--------|---------|
| `M-"` | split vertical | `C-b "` |
| `M-%` | split horizontal | `C-b %` |
| `M-!` | break pane | `C-b !` |
| `M-x` | kill pane | `C-b x` |
| `M-z` | zoom/unzoom | `C-b z` |
| `M-o` | next pane | `C-b o` |
| `M-;` | last pane | `C-b ;` |
| `M-q` | show pane numbers | `C-b q` |
| `M-m` | mark pane | `C-b m` |
| `M-M` | unmark pane | `C-b M` |
| `M-{` | swap pane up | `C-b {` |
| `M-}` | swap pane down | `C-b }` |
| — | rotate window | `C-b C-o` (3 keys) |
| — | rotate window -D | `C-b M-o` (conflicts `M-o`) |
| — | suspend client | `C-b C-z` (3 keys) |
| `M-h` | select pane left | `C-b Left` |
| `M-j` | select pane down | `C-b Down` |
| `M-k` | select pane up | `C-b Up` |
| `M-l` | select pane right | `C-b Right` |
| `M-Up` | resize up 5 | `C-b C-Up` |
| `M-Down` | resize down 5 | `C-b C-Down` |
| `M-Left` | resize left 5 | `C-b C-Left` |
| `M-Right` | resize right 5 | `C-b C-Right` |
| — | resize 1 cell | `C-b C-Arrow` (covered by `M-Arrow`) |
| — | refresh client (dir) | `C-b S-Arrow` (too many keys) |

### Layout

| Key | Action | Default |
|-----|--------|---------|
| `M-Space` | next layout | `C-b Space` |
| `M-E` | spread layout | `C-b E` |
| — | preset layouts | `C-b M-1..7` (conflicts `M-1..7`) |

### Windows

| Key | Action | Default |
|-----|--------|---------|
| `M-c` | new window | `C-b c` |
| `M-n` | next window | `C-b n` |
| `M-p` | previous window | `C-b p` |
| — | next window -a | `C-b M-n` (3 keys) |
| — | prev window -a | `C-b M-p` (3 keys) |
| `M-&` | kill window (confirm) | `C-b &` |
| `M-,` | rename window | `C-b ,` |
| `M-.` | move window | `C-b .` |
| `M-w` | window tree | `C-b w` |
| `M-f` | find window | `C-b f` |
| `M-'` | select window by index | `C-b '` |
| `M-0`–`M-9` | select window N | `C-b 0`–`C-b 9` |

### Sessions

| Key | Action | Default |
|-----|--------|---------|
| `M-s` | session tree | `C-b s` |
| `M-$` | rename session | `C-b $` |
| `M-d` | detach | `C-b d` |
| `M-D` | choose client | `C-b D` |
| `M-r` | refresh client | `C-b r` |
| `M-L` | switch to last session | `C-b L` |
| `M-(` | previous session | `C-b (` |
| `M-)` | next session | `C-b )` |

### Copy / scrollback

| Key | Action | Default |
|-----|--------|---------|
| `M-Enter` | copy mode | `C-b [` |
| `M-]` | paste | `C-b ]` |
| `M-=` | choose buffer | `C-b =` |
| `M-#` | list buffers | `C-b #` |
| `M--` | delete buffer | `C-b -` |
| `M-PageUp` | copy mode (scrolled up) | `C-b PPage` |

### Misc

| Key | Action | Default |
|-----|--------|---------|
| `M-:` | command prompt | `C-b :` |
| `M-?` | list keys | `C-b ?` |
| `M-/` | describe key | `C-b /` |
| `M-~` | message log | `C-b ~` |
| `M-i` | window info | `C-b i` |
| `M-t` | clock | `C-b t` |
| `M-C` | customize mode | `C-b C` |
| `M-Delete` | refresh client (clear) | `C-b DC` |

## Conflicts

These Alt keys are swallowed by tmux and won't reach your shell:

**High impact** — `M-c`, `M-d`, `M-f`, `M-Arrows` (word/paragraph navigation in readline)

**Medium** — `M-l`, `M-n`, `M-p`, `M-x`

**Low** — `M-h`, `M-j`, `M-k`, `M-t`, `M-Enter`

All Alt+symbol keys (`M-!`, `M-"`, `M-#`, etc.) are safe — rarely used in shells.
