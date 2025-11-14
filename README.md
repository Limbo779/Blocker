# Blocker

_Blocker_ is a productivity tool for Linux users that ensures distraction-free study sessions using Pomodoro timer logic by integrating with **Firefox** (using a dedicated study profile) and **Anki**.

## Features

- **Automatic Prompt**: Whenever you open Firefox or Anki, Blocker asks if you are about to study.
- **Pomodoro Timer**: On confirmation, starts a 50-minute Pomodoro timer (customizable).
- **Study Mode Firefox**: Opens Firefox in a dedicated "study" profile, blocking all other Firefox instances for the duration.
- **Manual Start**: You can start a Pomodoro session manually via CLI.
- **Session Lock**: Prevents multiple simultaneous study sessions.

---

## Getting Started

### Prerequisites

- **Python 3**
- Linux OS
- Firefox installed
- An existing Firefox profile named `study` ([Create profiles](https://support.mozilla.org/en-US/kb/profile-manager-create-and-remove-firefox-profiles))
- Python packages:
  ```bash
  pip install psutil
  ```

### Files Overview

- `process_monitor.py`: Monitors for Firefox/Anki startup and prompts for study session.
- `user_prompt.py`: Handles Yes/No GUI dialogs and Pomodoro time selection.
- `pomodoro_timer.py`: Displays a Pomodoro timer.
- `firefox_profile_manager.py`: Manages dedicated Firefox study profile and blocks other instances.
- `manual_launcher.py`: Allows starting a study session manually.
- `session_lock.py`: Manages session state to avoid conflicts.
- `Project.md`: Contains technical and architectural plan.

---

## Usage

### Automatic Monitoring

Simply run:
```bash
python process_monitor.py
```
Blocker will watch for "firefox" or "anki" to launch, and ask if you wish to start a study session.

### Manual Mode

Start a timer and study profile directly:
```bash
python manual_launcher.py --duration 90
```
(Default duration is 50 minutes if not specified.)

### Requirements

- You must have a Firefox profile named `study`:
  - Run: `firefox -P`
  - Create a new profile named `study`.
- Make sure you have Python 3 and the dependencies installed.

### How it works

1. **Detection**: When you start Firefox or Anki, Blocker asks if you're studying.
2. **Study Mode**: On "Yes," starts dedicated Firefox (study profile), blocks other instances, and runs a Pomodoro timer.
3. **Completion**: At timer end, regular Firefox use resumes.
4. **Manual Launch**: For flexibility, you can manually initiate the session.

## Troubleshooting

- Ensure the `psutil` package is installed.
- Ensure the lock file `/tmp/.study_pomodoro_lock` is writable.
- If Firefox doesn't open correctly, check your profile name.
- May require sudo/kill permissions for process management.

## License

MIT License

---

**Happy studying!**
