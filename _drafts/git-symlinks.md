Problem:

Windows doesnt copy symlinks by default

solution:
- enable symlinsk when installing git for windows
- ensure that core.symlinks is enabled in git config
- clone the repo as admin so it has permissions to create the symlinks
