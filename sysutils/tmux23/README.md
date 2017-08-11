# sysutils/tmux23

Backport tmux 2.3 because later versions only support UTF8,
that is not the default in FreeBSD.

This can cause breakage if we copy & paste in the shell.
