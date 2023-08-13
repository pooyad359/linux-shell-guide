# TMUX

tmux is a powerful terminal multiplexer that allows you to create, manage, and switch between multiple terminal sessions within a single terminal window.

Start a new session by simply running `tmux` in command line. `tmux` commands start by pressing `Ctrl` + `B` and the key related to the command. E.g., pressing `Ctrl` + `B` and the `c` will create a new window.

## Commands

### Windows

- `Ctrl` + `B`, `c`: Create a new window
- `Ctrl` + `B`, `d`: Detach from tmux session and run in the background
- `Ctrl` + `B`, `&`: Close the current window
- `Ctrl` + `B`, `,`: Rename the current window

### Panes

- `Ctrl` + `B`, `%`: Create a new pane by splitting the window horizontaly
- `Ctrl` + `B`, `"`: Create a new pane by splitting the window vertically
- `Ctrl` + `B`, `Ctrl` + `<Arrow>`: Resize a pane
- `Ctrl` + `B`, `x`: Close the current pane

### Navigation

- `Ctrl` + `B`, `NUM`: Switch to window number `NUM`
- `Ctrl` + `B`, `<Arrow>`: Switch between the panes
- `Ctrl` + `B`, `w`: List all windows and select one
- `Ctrl` + `B`, `;`: Toggle between the current and previous window
- `Ctrl` + `B`, `o`: Switch to the next pane

### Other

- `tmux ls`: List all tmux sessions
- `exit`: Close all windows and exit tmux

- `Ctrl` + `B`, `s`: List all windows
