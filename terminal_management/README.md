# Terminal Management

## TMUX

`sudo apt-get install tmux`

- Start: `tmux`
- Exit: (1) `ctrl + b` (2) press `x`, (3) press `y`
- Dettach: `ctrl +b` -> `d`
- Start a named session: `tmux new -s <name>`
- List of running sessions: `tmux ls`
- Split the window horizontally: `ctrl +b` -> `%`
- Split the window vertically: `ctrl +b` -> `"`
- Rename the window: `ctrl +b` -> `,`
- Go to next pane: `ctrl +b` -> `o`
- Toggle between two panes: `ctrl +b` -> `;`
- Switch window: `ctrl +b` -> `<window number>`
- Select window: `ctrl +b` -> `w`
- Re-attach a session: `tmux attach-session -t <name>`
