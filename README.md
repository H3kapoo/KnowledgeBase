# KnowledgeBase
---

## Table of contents
1. [Git](#git)
2. [OpenGL](#opengl)
3. [Windowing](#windowing)
4. [C/C++ VSCode configuration](#cc-vscode-configuration)
5. [Windows C/C++ configuration](#windows-cc-configuration)
6. [C/C++ useful commands](#cc-useful-commands)
7. [CMake](#Cmake)

---
### Git
Adding ```--help``` after each subcommand conveniently shows some small images of the flow some commands have.

#### Merge & Rebase
- Merge will just create a new commit on top of the destination branch that contains the changes from the last commit of the source branch.

- Rebase will try to replay all the commits from the source branch on top of the destination branch & new commit hashes will be generated.

Both can fail, but rebase keeps the history linear while merge gives you more history bloat.
```bash
  $ git merge <branch-from> <branch-into>
  $ git rebase <branch-from> <branch-into>
```

<details>
<summary>👉 Click here to expand</summary>
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/6a3b3c48-37e7-4105-8b0e-6091be6189ad" />
</details>


#### Pull
Pulls down and integrates the changes from remote into your local commits/changes. It usually asks for a strategy to integrate. 
```bash
  $ git pull <remote-name>
  $ git pull <remove-name> --rebase # Rebase is usually preferred in small projects, --merge otherwise
```

#### Fetch
Fetches changes from remote but it does not apply them locally just yet. ```git log``` will still show you that the HEAD is at your last local known commit.
```bash
  $ git fetch <remote-name>
```

#### Delete branch
You can delete a branch locally and/or on the remote as well.
```bash
  $ git branch -d <branch-name>               # delete only locally
  $ git push -d <remote-name> <branch-name>   # delete remotely as well
```

To actually apply the changes, reset the local HEAD to point to the end of the remote's branch (usually origin/master).
> **_NOTE:_** ⚠️ This will purge any changes you already have done locally. Commit them or something before this if needed.
```bash
  $ git reset --hard <remote-name>/<branch-name>
```

#### References
 - https://stackoverflow.com/questions/2530060/in-plain-english-what-does-git-reset-do
 - https://www.atlassian.com/git/tutorials/merging-vs-rebasing
---
### OpenGL
---
### Windowing
 - On Windows, right after creating a window a _FOCUS_ lost will immediately be sent to the previously focused window. Windows does not queue this event for the next poll to catch. Linux however does queue it.
 - On Windows, while mouse-resizing, the window enters in a _MODAL_ state in which no events can be sent in order to wake up the thread waiting on events. On Linux X11 however, this operation always wakes up the thread if it was explicily waiting for an event, windows doesn't spawn this "wake up" event.

---
### C/C++ VSCode configuration
---
### Windows C/C++ configuration
On Windows, the quickest way to get a C/C++ runtime and all the includes and such is to install MSYS2. It is basically a package manager.

Install the UCRT (universal C runtime) toolchain which is basically the modern Windows C runtime (```ucrtbase.dll```)
```bash
  $ pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
  $ g++ --version # check all ok
```

#### References
- https://github.com/msys2/msys2-installer/releases/
- https://code.visualstudio.com/docs/cpp/config-mingw
---
### C/C++ useful commands
#### Quickly show used include paths
Use if unsure where c/c++ compilers look for <includes> on the system by default
```bash
  $ <compiler> -v -E -x <lang> -
  $ g++ -v -E -x c++ -
```

#### References
- https://stackoverflow.com/questions/11946294/dump-include-paths-from-g
---
### CMake

