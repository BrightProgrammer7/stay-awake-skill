---
name: stay-awake
description: Prevent Mac from sleeping during long tasks. Use when running long operations, sync jobs, builds, or when user says "keep awake", "don't sleep", "stay awake", "prevent sleep", "caffeinate".
---

# Stay Awake

Prevent Mac from sleeping during long-running tasks.

## Commands

### Enable (prevent sleep)
```bash
caffeinate -i &
```

Or for persistent (survives terminal close):
```bash
sudo pmset -a disablesleep 1
```

### Disable (restore normal sleep)
```bash
pkill caffeinate
sudo pmset -a disablesleep 0
```

### Check status
```bash
pgrep caffeinate && echo "caffeinate running"
pmset -g | grep "sleep"
```

## Options

| Method | Survives terminal close | Needs sudo |
|--------|------------------------|------------|
| `caffeinate -i &` | No | No |
| `pmset disablesleep 1` | Yes | Yes |

## Flags

- `-i` — prevent idle sleep
- `-d` — prevent display sleep
- `-s` — prevent system sleep (AC power only)
- `-u` — declare user active

## Example: Keep awake for specific command
```bash
caffeinate -i long_running_command
```
