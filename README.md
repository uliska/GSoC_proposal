### Intro

Integrating version control into Frescobaldi has for a long time been on Frescobaldi's wish list. Power-users have already using version control tools such as git in their project management. It benefits a lot. The initial support has been implemented in the development version to allow developers to choose from which branch Frescobaldi is run.

I want to implement a version control system in Frescobaldi for users. After some research and discussion, I think a git based vcs is still the most appropriate choice,  which is also initially required  in the idea list.

In GSoC, I want to develop some vcs features with "git diff" as the core feature. With assist from these functions, a user is able to edit, stage, commit a LilyPond file seamlessly inside Frescobaldi.

### Project Goals

Git is the most widely version control system. 94 percent of vcs web search behavior is related to git[.](https://rhodecode.com/insights/version-control-systems-2016) And the format of git's output keeps consistent in different versions and platforms. This means that our concerns about complexity of cross-platform support and the work of maintenance can be reduced. The general way of implementing git based vcs is calling shell commands and interpreting the output. This way has been validated feasible through research on Sublime's Git plugins. So my work can be divided into two parts.
- Implementing the git module.
- Implementing the git GUI functions

#### Deliverables

Git command module. A module providing the git command interface for other modules. Including the following functionalities.
- a pure git command function.
    - cross-platform support
    - encode-decode support
    - asynchronous execution support
- basic git operations
    - get current branch
    - get current working file's git status
    - git diff (working vs Index, working vs HEAD, Index vs HEAD)
    - git commit
    - ...

Working view, Index view and HEAD view
- three views of current file and corresponding music views.
- optional: HEAD view and Index view will be shown from new created temp files. A caching system to cache LilyPond files and pdfs is considered.  
*(Comment (UL): I've had your demo running in my Frescobaldi since you made it available, and I see two problems: the cached files show up as "modified files" for Git, and they don't notice external changes. For example, if I change a branch externally or commit externally, they are not updated. This doesn't have to be considered in the proposal, but I wanted to point this out now instaed of later.)*

Git info
- display current file's git status: *untracked*, *unmodified*, *modified*, *staged*, *staged modified*
- display current branch

Git diff in gutter (Working vs. Index, Working vs. HEAD, Index vs. Working)
- Working vs. Index, Working vs. HEAD in Working view.
- Index vs. Working in Index view
- implement a new widget in sidebar rather than changing the numberarea module

Git diff inline
- extract the modified and deleted lines from "git diff" output and display them inline in the editor

Git diff inline editor (Working view)
- users can partially (in line or hunk) stage changes in Working view
- users can partially (in line or hunk) discard changes in Working view
- "Ctrl + z" undo operation support  
  *(Question: what do you mean with "undo" operation? If I'm not mistaken you haven't explained that yet in the email discussions)*

Git diff inline editor (Index view)
- users can partially (in line or hunk) unstage changes in Working view
- "Ctrl + z" undo operation support

Git commit
- provide a pop out window listing the staged files and asking for commit message for commit operation
- optional: display git diff in a meaningful way

#### If Time Allowed

Git blame
- display git blame information in the gutter (HEAD view)

Git based visual diff
- mark the diff scores in a pdf using diff results of the corresponding LilyPond file.

### Tentative Timeline

**May 4 - May 21**
- Read and tweak the code in *main.py mainwindow.py, layoutcontrol, musicview, vcs, sidebar, widgets*.
- Understand the structure of Frescobaldi. Learn to integrate a new module gracefully.
- Collect and discuss the details in implementing plan

**May 21 - May 29** Finalize on a work plan

There must not be any ambiguity relating to implementation details at this point of time

**May 30 - Jun. 11** Implement the "Git command module"

**Jun. 12 - Jun. 13** Test "Git command module" in different platforms.

By this time, it can provide following functions:
- check whether the working directory is git initialized
- get current branch
- get current file's git status (untracked, unmodified, modified, staged, modified staged)
- get current file's corresponding Index file and HEAD file
- get diff results of Working vs. Index, Working vs. HEAD, Index vs HEAD
- execute "git commit" command
- execute "git stage" command

**Jun. 14 - Jun. 15** Implement "Git info"

**Jun. 16 - Jun. 25** Implement "Git diff in gutter"

**Jun. 26 - Jun. 28** Phase 1 Evaluation

**Jun. 29 - Jun. 30** Buffer time

**Jun. 30 - Jul. 2** Implement the information extraction function of “Git diff inline”

By this time, we can extract new added, deleted, modified lines from "git diff" output. And we can get exactly which word is modified in modified lines.

**Jul. 3 - Jul. 5** Implement "Git diff inline" display

**Jul. 6 - Jul. 16** Implement  "Git diff inline editor (Working view)"

**Jul. 17 - Jul. 23** Implement "Git diff inline editor (Index view)"

By this time, we can call inline editors out in Working view and Index view.

**Jul. 24 - Jul. 26** Phase 2 Evaluation

**Jul. 27 - Jul. 28** Buffer time

**Jul. 29 - Aug. 2** Implement "Git commit"

**Aug. 3 - Aug. 13** Release test version to developers. Test functionalities in different environments.

**Aug. 14 - Aug. 20** Revise the code and bug fixes

**Aug. 21 - Aug. 29 Final Week** Buffer time

### About Me

I am Wen Xin, a first-year computer science graduate student at Beijing University of Posts and Telecommunications. I interned last year at Sogou, Inc., implementing score-following algorithms for music educational apps (c++, MATLAB) and learned about LilyPond from my colleagues who worked on developing music score interface.

### Links
- [Discussion in Fresobaldi's Forum](https://groups.google.com/forum/#!topic/frescobaldi/aQqBfeOz0Jg)

- [The demo of "git diff"](https://github.com/wenxin-bupt/frescobaldi/tree/git-diff-dev)
