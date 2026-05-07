# C-Shell: A Custom UNIX Shell

A robust, modular, and fully functional command-line interface (CLI) shell implemented entirely in C from scratch. This project mimics the core behaviors of traditional standard shells (like `bash` or `zsh`), introducing specialized built-in commands alongside advanced job control, I/O redirection, and inter-process communication via piping.

---

## Key Features

### 1. Advanced Process & Job Control
- **Background Processes (`&`):** Execute long-running tasks asynchronously in the background.
- **Job Management:** 
  - `activities`: List all currently running background processes.
  - `fg <pid>`: Bring a background process to the foreground.
  - `bg <pid>`: Resume a stopped background process.
  - `ping <pid> <signal>`: Transmit specific signals to processes directly from the shell.

### 2. Multi-Stage Piping & Redirection
- **Piping (`|`):** Supports chaining multiple commands together, effortlessly passing the standard output of one command as the standard input to the next (e.g., `cmd1 | cmd2 | cmd3`).
- **I/O Redirection (`<`, `>`, `>>`):** Route standard input/output to and from files seamlessly, allowing for overwriting (`>`) or appending (`>>`) data.

### 3. Custom Built-in Commands
- `hop`: A smart directory navigation tool (equivalent to `cd`).
- `reveal`: A robust directory listing and inspection tool (equivalent to `ls`).
- `log`: A persistent command history tracker that saves your session data to a local `.shell_log` file across restarts.

### 4. Robust Signal Handling
- Gracefully intercepts keyboard signals such as `SIGINT` (Ctrl+C) and `SIGTSTP` (Ctrl+Z), ensuring that the shell itself doesn't crash while managing child processes correctly.

---

## System Architecture & Implementation

The shell is designed with modularity in mind, cleanly separating input parsing, command execution, and signal management into distinct C source files (e.g., `parser.c`, `pipes.c`, `signals.c`).

The shell utilizes a raw input parser that tokenizes strings and offloads valid syntaxes to an executor module. It heavily leverages `fork()`, `execvp()`, POSIX file descriptors for piping, and `waitpid()` for process synchronization.

---

## Quick Start Guide

### Prerequisites
- A UNIX-based environment (Linux, macOS, or WSL).
- GCC Compiler and `make`.

### Build & Run
```bash
# Navigate to the project directory
cd C-Shell

# Compile the project using the provided Makefile
make

# Launch the custom shell (assuming the output binary is named 'shell' based on your makefile)
./shell
```

### Usage Examples
```bash
# Multi-stage piping and redirection
c-shell> reveal -l -a | grep "test" > output.txt

# Background process management
c-shell> sleep 10 &
[1] 12345
c-shell> activities
[1] 12345 : sleep 10 - Running
c-shell> fg 12345

# Persistent history
c-shell> log
c-shell> log execute 3
```

---

*This project demonstrates a deep understanding of Operating Systems concepts, memory management in C, and POSIX system programming.*
