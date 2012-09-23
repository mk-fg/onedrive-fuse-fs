skydrive-fuse-fs
----------------------------------------

Script to mount Microsoft SkyDrive folder as a FUSE filesystem.


Usage
----------------------------------------

Requires [python-skydrive](http://pypi.python.org/pypi/python-skydrive/) module
installed, use any of these lines:

	pip install 'python-skydrive[conf]'   # system-wide by default, probably needs root
	pip install --user 'python-skydrive[conf]'   # unprivileged install to ~/
	easy_install python-skydrive PyYAML   # try to avoid that one

("python-skydrive[conf]" installs python-skydrive + PyYAML, latter being is a
requirement for configuration-file handling in python-skydrive; install it in a
similar way if you're using `python setup.py install` or some older packaging
tools)

Usage from checkout (no installation - apart from aforementioned module(s) -
necessary), can be run from unprivileged user:

	% ./skydrivefs /mnt/skydrive

Install to system-wide $PATH (might need system-wide fusepy module as well):

	# pip install fusepy
	# install -m755 skydrivefs /usr/local/sbin/

Use from $PATH with `mount` command:

	# mount -t fuse.skydrivefs ~/.lcrc /mnt/skydrive

Examples with fstab(5) syntax (any one of these will do):

	/var/lib/skydrive.yaml /mnt/skydrive fuse.skydrivefs defaults 0 0
	/var/lib/skydrive.yaml:Pics /mnt/skydrive fuse.skydrivefs defaults 0 0

Available mount options can be found in `skydrivefs --help` output
(skydrive-specific) and `man mount.fuse` (more general fuse options).

Latter example mounts "Pics" SkyDrive folder instead of root.

Make sure configuration file (`/var/lib/skydrive.yaml` in fstab examples above)
is not accessible to anyone but root (or dedicated user), and is writable -
refreshed access tokens will be stored there.
