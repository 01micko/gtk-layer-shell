# GTK Layer Shell

![GTK Layer Shell demo screenshot](https://i.imgur.com/dIuYcBM.png)

A library to write [GTK](https://www.gtk.org/) applications that use [Layer Shell](https://github.com/swaywm/wlr-protocols/blob/master/unstable/wlr-layer-shell-unstable-v1.xml). Layer Shell is a Wayland protocol for desktop shell components, such as panels, notifications and wallpapers. You can use it to anchor your windows to a corner or edge of the output, or stretch them across the entire output. It supports all Layer Shell features including popups and popovers (GTK popups Just Work™). Please open issues for any bugs you come across.

## Supported platforms
This library only works on Wayland, and only on Wayland compositors that support the Layer Shell protcol. Layer shell __is supported__ on:
- wlroots based compositors (such as __Sway__)
- Mir-based compositors (some may not enable the protocol by default and require `--add-wayland-extension zwlr_layer_shell_v1`)

Layer shell __is not supported__ on:
- Gnome-on-Wayland
- Any X11 desktop

## Installing with your package manager
GTK Layer Shell is packaged for the following distros. If you've packaged it for a distro not listed, please make a PR or ask for it to be added in an issue.
- [Debian](https://packages.debian.org/source/sid/gtk-layer-shell) (>=11)
- [Ubuntu](https://packages.ubuntu.com/source/focal/gtk-layer-shell) (>=20.04)
- [Fedora](https://src.fedoraproject.org/rpms/gtk-layer-shell) (>=31)
- [Arch](https://www.archlinux.org/packages/community/x86_64/gtk-layer-shell/)
- [Gentoo](https://packages.gentoo.org/packages/gui-libs/gtk-layer-shell)
- [Alpine](https://pkgs.alpinelinux.org/package/edge/community/x86/gtk-layer-shell)
- [SUSE](https://packagehub.suse.com/packages/gtk-layer-shell/)

## Building from source
1. Clone this repo
2. Install build dependencies (see below)
3. `$ meson build -Dexamples=true -Ddocs=true -Dtests=true`
4. `$ ninja -C build`
5. `$ sudo ninja -C build install`
6. `$ sudo ldconfig`

### Build dependencies
* [Meson](https://mesonbuild.com/) (>=0.45.1)
* [libwayland](https://gitlab.freedesktop.org/wayland/wayland) (>=1.10.0)
* [GTK3](https://www.gtk.org/) (>=3.22.0)
* [GObject introspection](https://gitlab.gnome.org/GNOME/gobject-introspection/)
* [GTK Doc](https://www.gtk.org/gtk-doc/) (only required if docs are enabled)

To install these dependencies on Ubuntu 18.04 and later:
```
sudo apt install meson libwayland-dev libgtk-3-dev gobject-introspection libgirepository1.0-dev gtk-doc-tools
```

### Meson options
* `-Dexamples` (default `false`): If to build the example C apps; gtk-layer-demo is installed if examples are built; The Vala example is never built with the rest of the project
* `-Ddocs` (default `false`): If to generate the docs
* `-Dtests` (default `false`): If to build the tests

### Running the tests
* `ninja -C build test`

## Using the library
* `gtk-layer-demo` is installed if examples are enabled. Its UI exposes all features of the library, and it's useful for testing layer shell support in compositors
* [gtk-layer-shell.h](include/gtk-layer-shell.h) shows the full API, which can be used directly in C or C++
* [simple-example](examples/simple-example.c) is a minimal working C app
* [examples/demo/](examples/demo/) contains the code for `gtk-layer-demo` (a more complex app)
* The easiest way to build C and C++ apps is to use the `gtk-layer-shell-0` pkg-config package. Refer to your build system or the pkg-config docs for further instructions
* [examples/vala-standalone](examples/vala-standalone) contains a minimal working standalone Vala project, see [the readme](examples/vala-standalone/README.md) for details

## Licensing
GTK Layer Shell is licensed under the GNU Lesser General Public License version 3.0 or any later version.

Most of the individual source files are licensed under MIT.

To prevent possible future confusion, all contributions must contain the following in the PR message: *By opening this pull request, I agree for my modifications to be licensed under whatever licenses are indicated at the start of the files I modified*

### Licensing rationale
I want everyone to be able to use GTK Layer Shell however they desire, but parts of it are extracted from GTK. Therefore, the project as a whole is licensed under [GNU Lesser General Public License (LGPL) version 3](https://www.gnu.org/licenses/lgpl-3.0.en.html) or any later version (a newer version of the same license as GTK). See [LICENSE_LGPL.txt](LICENSE_LGPL.txt) and [LICENSE_GPL.txt](LICENSE_GPL.txt) for details. Almost all of the non-generated code, however, is licensed under [MIT](https://en.wikipedia.org/wiki/MIT_License) ([LICENSE_MIT.txt](LICENSE_MIT.txt)). At the top of each file should be a header that specifies which license applies to it. Please refer to that if in doubt.

### What this means for you
This library can be linked against under similar terms as GTK itself, so licensing shouldn't be a problem for most potential users. Furthermore, most of the code within this library can be used in permissively licensed or proprietary projects.
