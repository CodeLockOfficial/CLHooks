# CodeLocked Repository Setup

This document outlines how to set up the necessary hooks in your `CodeLocked` repository.

## Setting Up Git Hooks

To use the custom Git hooks for your repository, follow these steps:

1. Navigate to the `.git/hooks` folder in your repository.
2. Place the `pre-push` and `pre-push.ps1` or `pre-push.py` (depending on your environment) files into the `.git/hooks` folder.
3. Ensure that the scripts are executable. On Unix-like systems, you can run `chmod +x pre-push pre-push.ps1` or `chmod +x pre-push pre-push.py`.

These hooks will now be executed as part of your Git workflow, enforcing any checks or standards defined within them prior to pushing code.

## Troubleshooting

### Issue: `pip not found`

#### Description

When attempting to run scripts or commands that rely on `pip`, you might encounter an error indicating that `pip` is not found. This issue can arise in environments where `pip` is not recognized as the command for the Python package installer, but `pip3` is instead.

#### Resolution

To resolve this issue, modify the script where the error occurs by changing the command that invokes `pip` to use `pip3` instead. Here's how:

- Locate the script causing the issue, typically involved in a pre-commit or pre-push hook.
- Open the script in a text editor.
- Find the line attempting to call `pip`. It will look something like this:
  ```python
  subprocess.check_call([sys.executable, "-m", "pip", "install", package], stdout=subprocess.DEVNULL)```
- Modify this line to:
```
subprocess.check_call([sys.executable, "-m", "pip3", "install", package], stdout=subprocess.DEVNULL)
```
- Save the file and re-run.
- This modification instructs the script to use pip3, the command specifically associated with pip installations in Python 3 environments, effectively resolving the pip not found error.

### Issue: I cannot find my .git folder
### Description
When looking for the .git folder in your local repository, you might notice that it does not appear to exist. This is because by default, all directories with the `.` prefix are hidden from the user. 

### Resolution

To resolve this issue, change your settings to show `hidden files`. 

On Windows:
- If using the file explorer, click on the `View` button in the file explorer toolbar
- Hover your cursor over the `Show` field
- Check the `Hidden Items` field

On MacOS:
- Open Finder.
- Press Command+Shift+. (dot). This will toggle the visibility of hidden files in Finder.

On Linux
- Open terminal
- Navigate to your repository directory
- Run `ls -a`
- Or simply `cd .git/hooks`
