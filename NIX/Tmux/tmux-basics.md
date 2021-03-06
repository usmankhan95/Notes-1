# Typical Tmux Commands

Tmux commands and shortcuts. Some of the shortcuts such as the pane resizing shortcuts are not the default bindings, these notes are specific to the linked configuration.

Basics & Titbits:

* Leader key (LK) default binding: `C-b`
* LK rebound to: ``` ` ```
* Tmux configuration [here](https://github.com/JoshDoug/dotfiles/blob/master/.tmux.conf).
* Tmux version: `tmux -V`, no idea why but it needs to be a capital V, who cares about consistency or convention right?
* List shortcuts: `LK ?`
* Clock: `LK t`

## Tmux Sessions

To start a new session, just run `tmux`. The session number is shown at the bottom left of the window, like so: `[0]`.

* Detach from a session: `LK d`
* List sessions: `tmux ls`
* Attach to a session:
  * If only a single session exists: `tmux attach`, this will also connect to the most recently used session.
  * List sessions and select the name or number: `tmux attach -t 2`, or `tmux attach -t working` for a session named working.
* Rename session: `LK $`, this is done from within a session.
* List and select sessions from within tmux: `LK s`, this gives a list of sessions that allows for easy switching between sessions.
* Kill a session: `tmux kill-session -t n`, where n is the name or number of the session. Detach from the session to be killed first, although it can still be done from within another tmux session.

## Tmux Windows

* Create window: `LK c`
* Name the current window: `LK ,`
* Switch to next or previous window: `LK n` for next window, `LK p` for previous window, or rebound to `Shift Left` to move left or `Shift Right` to move right, which can be used to loop through all the windows of a session.
* Switch to the last used window: `LK l`
* Close window: `LK &`, this will ask for confirmation and then close any panes within the window.
* List windows: `LK w`, this will list the windows which can be navigated by arrow keys and selected with enter. Newer tmux version show a preview of the window

## Tmux panes

* Vertical split pane: `LK |` (includes Shift for the pipe symbol), or `LK "`
* Horizontal split pane: `LK -`, or `LK %`
* Resize panes to the left, down, up, right: `alt h`, `alt j`, `alt k`, `alt l`, where alt and letter can both be held to instead of repeatedly being pressed.
* Cycle through panes: `LK o`
* Move to specific panes: `LK arrow key`
* Switch between two most recently used panes: `LK ;`
* Cycle the content of each pane with `LK C-o`, where `LK` and `C-o` can be pressed consecutively instead of all at once which would be annoying.
* Other shortcuts to resize panes: `LK C-arrow key`, this is a default and doesn't work well on macOS which uses that are an OS shortcut for switching applications windows or spaces.
* Resize panes in larger increments: `LK Esc-arrow key`, this is also a default that doesn't work well on macOS.
* Promote pane to its own window: `LK !`
* Kill/close pane: `LK x`

## Tmux CLI

The Tmux Commandline Interface can be used to run more complex commands to interact with panes, windows, and sessions, as well as set options on tmux itself. Everything (probably) doable via a keyboard shortcut can be done with the more verbose Tmux CLI, but there are some things that can only be done via the CLI (or possibly the .tmux.conf).
To access the tmux CLI: `LK :`, need to use shift otherwise it would be a semi-colon.

* New named window: `:new-window -n name`
* Start window in a specific folder: `:new-window -c /some/folder`
* Set windows to monitor activity: `:set-option -g monitor-activity on`