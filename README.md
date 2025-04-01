# test-repo-version-update

# Host Code
# Host Code


This repository is to store the full source that is used to create builds for use on the Main Raspberry Pi.

**Do not** share or distribute any part of this source code with anybody unless they have access to this repository. If you are unsure, ask a GitHub admin.

## Index
- [Repository Usage](#repository-usage)
- [Frequently Asked Questions](#frequently-asked-questions)
- [Contributing](#contributing)
- [Support](#support)

## Repository Usage
This repository contains both the Decawave Tag API as well as the actual C and Python source for the bot. The bot source is located under:
```
examples/ex1_TWR_4Hosts/src
```
Any changes required can be made there. Do not push any garbage files to this repository unless they are absolutely necessary to the bot functionality or build procedure!

To run the source code, you must provide the path to the dynamic linker which searches for *libBOT4.so*. When running with sudo, the environment is different from the user and any environment variables have to be set again before running anything. Use the following command to run the source:
```
sudo LD_LIBRARY_PATH=/home/runner/work/test-repo-version-update/test-repo-version-update python3 BOT4.py
```

To create a build, make sure you have the PyInstaller Python package and then run:
```
make clean
make
pyinstaller --onefile --add-binary 'libBOT2.so:.' BOT4.py
```
Linux terminal commands can be separated by a semicolon. This allows you to run multiple commands on the same line.

For a one-liner that guarantees you have the latest C changes included in the build, run:
```
make clean; make; pyinstaller --onefile --add-binary 'libBOT2.so:.' BOT4.py
```
Just make sure that there are no errors during the make, otherwise the build will fail!

To transfer the newly created build to a bot, run:
```

```
For example:
```
scp dist/BOT2 pi@192.168.0.211:~/HOST_SW_HASW2.2_Alpha_3
```
and input the password if prompted.

## Frequently Asked Questions
> Q. *scp is giving me a "REMOTE HOST IDENTIFICATION HAS CHANGED" error. What should I do?*

Run the command:
```
ssh-keygen -R <Problematic IP>
```
and then try the scp command again. You will need to enter "yes" when prompted.

> Q. *I changed code in one of the .h files and did a make, but the compiler shows libBOT4.so is up to date!*

Simply run:
```
make clean
```
to clean up the existing *libBOT2.so* file and then run make again to create the updated *libBOT4.so* file.

> Q. *How do I run this code on my laptop?*

You can't. This code has RPi-specific dependencies and must be run on a Raspberry Pi or it will not even get past the first few imports.

> Q. *How do I run this code on a Raspberry Pi?*

> Q. *How do I create a build?*

> Q. *How do I transfer the created build to the bot?*

Go through the [Repository Usage](#repository-usage) section. It has all the necessary instructions to help answer these questions.

## Contributing
As a rule of thumb, **do not** directly push to main. Create a branch with the feature that is in development or the bug fix and create a pull request for the same. The changes will be reviewed and then merged into the main branch as soon as possible.

Don't forget to run:
```
make clean
make
```
in the *src* folder before pushing to this repository, so that any C code changes that have been made also get reflected in the *libBOT4.so* file.

## Support
Ask any of the GitHub administrators for help if you have any queries about how this repository is to be used or Git-specific doubts that you need answers to.

