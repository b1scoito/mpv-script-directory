A machine-readable directory of scripts and other tools for mpv.

Why
===
Mpv is a great free and open video player. It has interfaces to extend
it with different types of scripts. There is a large number of those
scripts, many of them of great use. A [wiki page](https://github.com/mpv-player/mpv/wiki/User-Scripts) lists them, but
browsing this is tedious and installing and updating scripts was not
comfortable. Therefore, I created this directory as backend for a new
[plugin manager](https://github.com/Nudin/mplug).

How does it work
================
The main file of this project ist `mpv_script_directory.json`. It contains all
the known tools with their metadata. The Information is encoded as JSON:
- The file contains an object (aka dictionary) where each tool is represented as one value.
- The keys in this object are identifiers that have to be unique. They are for
  github and gitlab they are well-defined, otherwise they are derived from the
  projects url.
- Every script is described by an object with the following keys:
	- `name`: The name of the tool
	- `url`: The url of the project
	- `type`: The type of the tool:
		- `javascript`
		- `lua script`
		- `user shader`
		- `vapourSynth scripts`
		- `C plugin`
		- `other`
	- `desc`: A short description of the tool
	- `os`: A List of the supported operating systems, an empty list is
	  interpreted as platform independent.
	- `stars`: The number of stars the project's repository has on github/gitlab
	- `sharedrepo`: Boolean, `True` if the tool shares a repository with other tools
	- `install`: Install method, currently only `git` is supported
	- `git`: If `install` is `git` this should be set to the cloneable url
	- `gitdir`: Name for local directory to clone the git repo in. Needed
	  to support scripts sharing a git repo.
	- `scriptfiles`: List of files from source that should be installed in
	  the script folder.
- The directory is initially created by scraping the [wiki page](https://github.com/mpv-player/mpv/wiki/User-Scripts). This is done by
  `scrapewiki.py` – in the future the directory should be updated directly and
  the scraping script should therefore become obsolete. Maybe it can be
  continued to be used to check for divergence from the wiki page.
- The script `querystars.py` checks the number of stars the project has, if it
  is hosted on github, github gist or gitlab.com. Other fields are not modified.

Usage
=====
- [MPlug](https://github.com/Nudin/mplug) is a plugin manager for mpv, it can install plugins from this directory.
	- Note: For this to work, the directory needs to contain install
	  instructions. Those are currently still missing for most plugins, but can
	  be added very easily.
- There is a [Proof-of-Concept webpage](https://nudin.github.io/mpv-script-directory/) that allows searching, sorting and
  filtering the directory.
- This list can be read with any JSON parser.


ToDo
====
There's a lot to do – please help!
- Add further fields: `screenshot`, `deprecated`, `superseededby`, …
- Add more install methods: `tar`, `url`, `hg`, …
- Add support for other file types then scripts: `shaders`, `config`, …
- Fill the install introductions for all tools
- Set up an automatic update of the star counts
- Improve the web version
- Tell the world!
