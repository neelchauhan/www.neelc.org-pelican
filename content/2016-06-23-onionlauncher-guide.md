Title: OnionLauncher Guide
Date: 2016-06-23 11:00
Category: Software
Tags: onionlauncher, tor, software

[OnionLauncher](https://github.com/neelchauhan/OnionLauncher) is a launcher for
the Internet anonomity software [Tor](https://www.torproject.org/) using
[Python](https://www.python.org/),
[PyQt5](https://riverbankcomputing.com/software/pyqt/intro), and
[Stem](https://stem.torproject.org/). It is similar to a prevoius project I
done ([TorNova](https://github.com/neelchauhan/TorNova)), but is different in
some aspects.

But the point of this article is to serve as a guide for OnionLauncher.

First, you should make sure that you have all the dependencies installed. The
installation varies between operating systems and distributions so I don't plan
to cover it here. You will also need to have `tor` in your `$PATH` which won't
be covered either. I will cover how to run OnionLauncher from two methods: from
the source directory and if you installed it through `setup.py` or a packaging
manager (like `apt-get` or `pacman`).

If you are running OnionLauncher from the source directory, you can launch it
with something like this:

	$ cd OnionLauncher/
	$ python main.py

Replace `python` with the name and location of your Python intepreter.

If you have installed OnionLauncher from `setup.py` or a packaging manager,
you can just run OnionLauncher like this:

	$ OnionLauncher

I'm assuming you are on a Unix-like system if you used this method as I have
not run OnionLauncher on Windows with `setup.py`.

After you have opened OnionLauncher, you should get a window that looks like
this:

![OnionLauncher Screenshot]({filename}/images/OnionLauncher/main.png)

To start Tor with the default settings, you can just press **Start Tor**. Keep
in mind that may take a few seconds to start. To stop Tor, you can press **Stop
Tor**. Keep in mind that to the right of the **(Start/Stop) Tor** button, there
is a label that mentions whether Tor is running or not.

OnionLauncher allows you to specify options (although it can't save them, for
now at least). Clicking on the **+** button on the bottom left allows you to
add a row. In the newly created row, you can specify an option in the
**Setting** row and the parameter of the option you want to set in the
**Parameter** row. If a option includes spaces, you need to add it in the
**Setting** row (It worked better for me).

To remove an option, select a row, or a column from the row you want to delete,
and then press the **-** button.

And that's all, or atleast for the current moment it is.
