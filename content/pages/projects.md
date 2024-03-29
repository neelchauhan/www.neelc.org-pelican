Title: Projects

Here, I will describe projects I am actively working on, or have worked on.
This list excludes [school](http://engineering.nyu.edu/) projects.

## Current Projects

### FreeBSD Ports

[FreeBSD Ports](https://www.freebsd.org/ports/) is
[FreeBSD's](https://www.freebsd.org/) package management system (like `apt-get`
is on [Debian](https://www.debian.org/) and [Ubuntu](http://www.ubuntu.com/)).
I maintain
[various packages](https://www.freshports.org/search.php?stype=maintainer&method=exact&query=neel@neelc.org)
for FreeBSD Ports including
[Keras](https://keras.io/) and [Nestopia](http://0ldsk00l.ca/nestopia/), and
contributed updates to others, such as
[Tor](https://www.torproject.org/), [Knot DNS](https://www.knot-dns.cz/),
and [Requests](http://docs.python-requests.org/en/master/).

A list of FreeBSD Ports contributions I have made are available
<a href="http://freshbsd.org/search?project=freebsd-ports&q=Neel+Chauhan">
at the BSD source code tracking site FreshBSD</a>.

### The Tor Project

I recently also started to contribute to [Tor](https://www.torproject.org/), a
popular Internet anonymity service. My contributions can be seen at
[Tor's Git repository](https://gitweb.torproject.org/tor.git/log/?qt=author&q=Neel+Chauhan).

## Previous Projects

Keep in mind that I may do sporadic work on these projects.

### MiniMiniWeb

[MiniMiniWeb](https://github.com/neelchauhan/MiniMiniWeb) is a minimal,
multithreaded web server written in C designed for Unix-like systems.

### OnionLauncher

[OnionLauncher](https://github.com/neelchauhan/OnionLauncher) is a launcher for
Tor written in Python, and uses [Stem](https://stem.torproject.org/) and
[PyQt5](https://www.riverbankcomputing.com/software/pyqt/download5).
OnionLauncher targets both Windows and Unix-like systems

### TorNova

[TorNova](https://github.com/neelchauhan/TorNova), the predecessor to
OnionLauncher, is a frontend for Tor written in Python using
[Stem](https://stem.torproject.org/), [GTK+ 3](http://www.gtk.org/)
and [PyGObject](wiki.gnome.org/PyGObject). Unlike OnionLauncher, TorNova
primarily targeted Unix-like systems and had a few built-in features such as
logfile and circuit viewing.

### currtime

[currtime](https://github.com/neelchauhan/currtime) is a real time command line
clock written in C, and is targeted primarily for Unix-like systems (although
it can run on Windows with [Cygwin](https://www.cygwin.com/)) because currtime
relies on Unix system calls.

### colwide

[colwide](https://github.com/neelchauhan/colwide) is a Perl script which
displays a specified number of characters (default: 80 `#` characters) on the
terminal. It was used primarily for aligning terminals with
[tmux](https://tmux.github.io/) (because I want my terminals to all be
perfectly 80 characters).
