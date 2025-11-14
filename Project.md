## Goal

- whenever i open Firefox or anki the program should ask whether I'm gonna a study. i use linux machine
- if i said yes , it will start 50 min pomorodo timer till the time i specified and open a different firefox profile and never let me open another one
- if i said no , it won't do anything 
- i should be able to run the program myself too

Here is a detailed coding plan that includes necessary tools:

## Coding Plan

### 1. Monitor Application Launch (Firefox/Anki)
- Use a process monitoring approach to detect when Firefox or Anki starts.
- Poll the process list regularly (e.g., every few seconds) or hook system-level events.
- Tools: `psutil` for cross-platform process detection.

### 2. GUI Prompt on Launch
- When Firefox or Anki is detected running, prompt user with a Yes/No dialog asking if they are going to study.
- Tools: `tkinter` or `easygui` for simple Yes/No dialog.

### 3. Pomodoro Timer Logic
- If user says "Yes," start a Pomodoro timer (default 50 minutes or user-specified duration).
- Provide timer countdown (optional popup or console output).
- Tools: `tkinter` for GUI timer or simple console timer.

### 4. Open Different Firefox Profile and Restrict Other Instances
- Open a separate Firefox profile dedicated for study.
- Prevent opening of other Firefox profiles or normal Firefox windows during the Pomodoro session.
- On pomodoro end or cancel, allow normal Firefox instances again.
- Tools:
  - Firefox command-line with `-P` (profile) argument to launch specific profiles.
  - `subprocess` to open Firefox with specific profile.
  - Process control with `psutil` to monitor and kill or block other Firefox instances.
  - Possibly use a mutex or flag file to indicate session active.

### 5. No Action on "No" Response
- If user says no, do nothing and allow normal usage.

### 6. Manual Run Option
- The program should function independently as well, allowing user to start the Pomodoro and study profile anytime manually.
- Provide a simple main menu or command line interface to start study session manually.

***

## Tools and Libraries Needed

| Feature                         | Recommended Tools/Libraries                   |
|--------------------------------|----------------------------------------------|
| Process detection              | `psutil`                                    |
| GUI prompt Yes/No dialog       | `tkinter` or `easygui`                       |
| Pomodoro timer                 | `tkinter` or simple time/sleep for countdown|
| Open Firefox with profile       | `subprocess`, Firefox CLI with `-P` option  |
| Control running Firefox instances| `psutil` (to monitor/kill processes)       |
| Single instance check (optional)| Lock/mutex or flag file mechanism            |

***

## Files to be Coded 

- process_monitor.py : Continuously monitors system processes to detect when Firefox or Anki launches, then triggers the user prompt.

- user_prompt.py : Displays a Yes/No dialog asking if the user is going to study; returns the user's response.

- pomodoro_timer.py : Runs and displays a Pomodoro countdown timer; manages start, pause, and end of the timer session.

- firefox_profile_manager.py : Opens Firefox with the specified study profile and prevents other Firefox instances from opening during the study session.

- manual_launcher.py : Provides a manual interface or command-line tool to start or stop the study session and Pomodoro timer independently of process detection.

- session_lock.py : Manages a lock or flag to indicate whether a Pomodoro session is active, preventing multiple simultaneous sessions or conflicts.

