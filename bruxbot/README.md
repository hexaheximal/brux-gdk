# bruxbot

This is the code for the custom buildbot (made by [@hexaheximal](https://github.com/hexaheximal)) used in Brux GDK.  

The frontend (written in Go, currently doesn't exist yet) provides a web interface for autobuilds, while the backend (written as POSIX shell scripts) does the real building.  

It works by bootstrapping a custom toolchain and building Brux GDK with it. It's basically it's own tiny distro.  

Please note that Kelvin has previously [stated](https://clips.twitch.tv/SpicyZanyCaterpillarPogChamp-Ww4Fb3fED04VGK8H) that he doesn't really understand how linux distros work, so you really shouldn't ask him about bruxbot - the response you'd get would probably be confusion.  

I currently don't have write access to the upstream repository though, so bruxbot contributions should go to [hexaheximal's bruxbot branch](https://github.com/hexaheximal/brux-gdk/tree/bruxbot).

**If you're going to use this on a computer that isn't very good, I hope you're prepared to wait hours to bootstrap this...**

The toolchain is really large too - For a generic x86_64 toolchain, the toolchain directory alone is 1.8GB and the entire workdir is 11.3GB.

Once you finish bootstrapping the toolchain though, it's reasonably fast to build brux-gdk with it.

The idea with using a custom toolchain is that we can not only support a lot of architectures but also be able to have a lot of compatibility by manually choosing the glibc version, however it currently just uses the latest version of everything.  

Additionally, this really should be using a chroot, but it currently doesn't.  

## Known issues

- CMake links the libraries using the toolchain directory, so it's broken on the target system but should work fine on the build machine.
- Cross-compiling to a different architecture is probably completely broken, although I haven't tested it.
- Brux GDK fails to load and then later segfaults due to missing SDL_image libraries.