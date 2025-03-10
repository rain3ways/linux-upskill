# Day 5 - More or less

## Objectives
- Gain a quick understanding of essential Linux topics: tab completion, command history, reading dot files, customizing the prompt, and viewing files with `more` and `less`.
- Build foundational skills for future practice sessions without requiring immediate mastery.

## Basic Commands Practiced

| Command       | Description                                   | Usage Example          |
|---------------|-----------------------------------------------|------------------------|
| `less`        | View file contents page by page               | `less /etc/services`   |
| `more`        | View file contents (fewer navigation options) | `more .bashrc`         |
| `history`     | Display cached command history                | `history`              |
| `!n`          | Repeat command number `n` from history        | `!20`                  |
| `Ctrl + r`    | Search through command history                | `Ctrl + r`, then type  |
| `ls -la`      | List all files, including hidden ones         | `ls -la`               |
| `nano`        | Open the nano text editor                     | `nano summary.txt`     |

## Lessons and Notes
1. **Tab Completion**: Speeds up command entry and reduces errors by auto-completing commands and file names (e.g., `les` + `Tab` becomes `less`).
2. **Command History**: A powerful tool for recalling and reusing past commands, especially useful for complex or repetitive tasks.
3. **Dot Files**: Hidden files (starting with `.`) in your home directory store personal settings, like `.bashrc` for shell configuration and `.bash_history` for command history.
4. **Prompt Customization**: Adjusting the shell prompt (via `PS1`) enhances usability and personalizes your terminal experience.
5. **File Viewing**: `more` and `less` are essential for navigating large files; `less` offers more features, like searching and jumping to the top/bottom.
6. **Practice Matters**: These commands may seem simple, but they’re widely used by system administrators daily—mastery comes with time.

## Issues Encountered and Solutions
- **Issue**: Couldn’t see hidden files in the home directory.  
  **Solution**: Used `ls -la` to list all files, including those starting with a `.` (e.g., `.bashrc`).
- **Issue**: Forgot previously used commands.  
  **Solution**: Ran `history` to view past commands and used `Ctrl + r` to search for specific ones interactively.
- **Issue**: Ambiguity with tab completion (e.g., multiple files match).  
  **Solution**: Pressed `Tab` twice to display all matching options, then typed more characters to narrow it down.

![Troubleshooting](/screenshots/day-5/Troubleshooting.png)

### References
- [Nano editor tutorials](/http://www.debianadmin.com/nano-editor-tutorials.html)
- [Unix Less Command: 10 Tips for Effective Navigation](/http://www.thegeekstuff.com/2010/02/unix-less-command-10-tips-for-effective-navigation/)
- [How To Use Bash History Commands and Expansions…](https://www.digitalocean.com/community/tutorials/how-to-use-bash-history-commands-and-expansions-on-a-linux-vps)
- [Bash Shell: Take Control of PS1, PS2, PS3, PS4 and PROMPT_COMMAND](http://www.thegeekstuff.com/2008/09/bash-shell-take-control-of-ps1-ps2-ps3-ps4-and-prompt_command/)