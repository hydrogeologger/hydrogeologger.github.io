---
layout: post
title: 2017-08-15-install-linux-on-mac.md
---
1. make refind having access to debian 2017-08-15 
  EFI is considered to be the replacement for bios. run the following commands on debian machine:
{% highlight bash %}
grub-install /dev/sda5
update-grub
efibootmgr -c -d /dev/sda5 -p 1 -w -L debian -l \EFI\debian\grubx64.efi
efibootmgr --verbose
{% endhighlight %}
  It needs to be noticed that in some cases 1. the screen appears to be black 2. nothings was happening after seleting debian. for the two sympoton, just try to wait patiently, and perhapse try to increase the back light(f2).

<<<<<<< HEAD
=======
2. use 
>>>>>>> 5d47d68d445d1fbbfcd973c0200875e2fe99c004
