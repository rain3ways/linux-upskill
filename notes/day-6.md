# Day 6 - Editing with “vim”

## Objectives
- Learn `vi` and `vim`, the go-to editors on Linux.
- Master basic `vim` commands and modes.
- Start with `vimtutor` and edit a file hands-on.
- Build a solid base to use `vim` like a pro sysadmin.
## Basic Commands Practiced

| Command       | What It Does                            | How to Use It         |
|---------------|-----------------------------------------|-----------------------|
| `Esc Esc`     | Back to normal mode                     | Hit `Esc` twice       |
| `:q!`         | Quit, no save                           | `:q!` + `Enter`       |
| `:w`          | Save                                    | `:w` + `Enter`        |
| `:wq`         | Save and quit                           | `:wq` + `Enter`       |
| `h j k l`     | Move cursor (left, down, up, right)     | Just press `h`, `j`   |
| Arrow keys    | Move cursor (if they work)              | Use arrows            |
| `u`           | Undo                                    | `u` in normal mode    |
| `dd`          | Delete line                             | `dd` in normal        |
| `33dd`        | Delete 33 lines                         | `33dd` in normal      |
| `P`           | Paste                                   | `P` in normal         |
| `/pattern`    | Search                                  | `/sun` + `Enter`      |
| `n`           | Next match                              | `n` after search      |
| `G`           | Jump to file end                        | `G` in normal         |
| `gg`          | Jump to file start                      | `gg` in normal        |
| `i`           | Start typing                            | `i` in normal         |

## Lessons and Notes

### Why Bother with Vim?
- It’s everywhere on Linux—can’t escape it as a DevOps
- Super powerful once you get it; beats mousing around.
- Pros expect you to know it, so it’s a must.
### First Steps
- Check: `vi --version`. If it says `vim`, you’re set.
- Try `vimtutor`—it’s a quick, hands-on intro.
- Copy `/etc/services` to `testfile`, then edit with `vim`.

![Vimtutor](/screenshots/day-6/vimtutor-demo.png)

### The Basics
- **Modes:** Normal (commands) and Insert (typing). `Esc Esc` gets you back to normal.
- **Flow:** Open with `vim testfile`, move with `h j k l`, edit with `i`, save with `:w`, exit with `:wq`.
### Quick Tips
- Mess up? `u` undoes it.
- Find stuff: `/pattern`, then `n` for next.
- Cut with `dd`, paste with `P`.
- Jump around: `G` to end, `gg` to start.
### Why Not Nano?
- `vi` is always there; `nano` isn’t.
- `vim` screams “I know my stuff.”
- More tricks up its sleeve for fast edits.

## References
- [How to Copy, Cut and Paste in Vim / Vi](https://linuxize.com/post/how-to-copy-cut-paste-in-vim/)
- [Practice Vim with an interactive tutorial](https://openvim.com/index.html)