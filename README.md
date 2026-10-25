# stay-awake

A [Claude Code](https://claude.com/claude-code) skill that keeps your Mac from sleeping during long tasks: builds, syncs, model runs, anything that dies when the lid logic kicks in.

Say "stay awake", "keep awake", "don't sleep" or "caffeinate" and Claude runs the right command for you.

**macOS only.** It uses the built-in `caffeinate` and `pmset` tools. No dependencies.

## Install

```bash
git clone https://github.com/BrightProgrammer7/stay-awake-skill.git
mkdir -p ~/.claude/skills/stay-awake
cp stay-awake-skill/SKILL.md ~/.claude/skills/stay-awake/
```

Restart Claude Code. The skill shows up as `/stay-awake`.

## Usage

In Claude Code:

```
/stay-awake
```

Or just ask: "keep my Mac awake while this build runs".

## What it runs

| Method | Command | Survives terminal close | Needs sudo |
|--------|---------|------------------------|------------|
| Temporary | `caffeinate -i &` | No | No |
| Persistent | `sudo pmset -a disablesleep 1` | Yes | Yes |

Turn it off:

```bash
pkill caffeinate
sudo pmset -a disablesleep 0
```

Check status:

```bash
pgrep caffeinate && echo "caffeinate running"
pmset -g | grep "sleep"
```

Wrap one command so the Mac stays awake only while it runs:

```bash
caffeinate -i long_running_command
```

### `caffeinate` flags

- `-i` prevent idle sleep
- `-d` prevent display sleep
- `-s` prevent system sleep (AC power only)
- `-u` declare the user active

## Warning

`pmset disablesleep 1` persists across reboots until you set it back to `0`. Forget it and your laptop stays awake in your bag. Prefer `caffeinate` unless the task must outlive the terminal.

## License

MIT
