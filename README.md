# Installing gtk4 or gtk+ successfully in 2024 !
How to install successfuly `gtk4` on Linux ?
# How to install packages or librairy for Linux from scratch using source ?
Almost all the packages to be installed such as `gtk4` are not binaries but in source form.
So, it is important to know how to install them given their source code.

## Installing a package from source typically involves the following steps:

1. **Download the Source Code:**
   - Visit the official website of the software or library you want to install.
   - Look for a "Downloads" or "Source Code" section.
   - Download the source code archive (usually a .tar.gz or .zip file).

2. **Extract the Source Code:**
   - Use a file archiver or terminal to extract the contents of the downloaded archive.
     ```bash
     tar -xzvf filename.tar.gz
     ```

3. **Navigate to the Source Directory:**
   - Use the terminal to go into the directory where the source code is extracted.
     ```bash
     cd extracted_directory
     ```

4. **Read the Documentation:**
   - Look for a file named `README` or `INSTALL` in the extracted directory.
   - Read the documentation to find information about dependencies, build instructions, and installation steps.

5. **Install Dependencies:**
   - If the software has dependencies, install them first. Use your system's package manager to install development libraries and tools required for building the software.

6. **Configure the Build:**
   - Run the configure script to check the system for dependencies and set up the build environment.
     ```bash
     ./configure
     ```

7. **Compile the Code:**
   - Use a build tool (commonly `make`) to compile the source code.
     ```bash
     make
     ```

8. **Install the Software:**
   - Install the compiled binaries and related files to the system.
     ```bash
     sudo make install
     ```

   - Note: The `sudo` command is used to gain administrative privileges for the installation. It might prompt you to enter your password.

9. **Clean Up (Optional):**
   - After installation, you can clean up the build artifacts.
     ```bash
     make clean
     ```

   - This step is optional but can save disk space.

10. **Verify the Installation:**
    - Ensure that the software is installed correctly by running it or checking its version.
    ```bash
    command_name --version
    ```

Remember, the specific steps might vary depending on the software and your operating system. Always refer to the documentation provided with the source code for accurate and detailed instructions. Additionally, installing packages from source can introduce complexities, and it's usually recommended to use your system's package manager whenever possible to manage software installations and updates.

# Installing gtk4 (2024 current version : 4.9.4)

GTK (GIMP Toolkit) is a library for creating graphical user interfaces (GUIs). It provides a set of tools and widgets that developers can use to build interactive and visually appealing applications. GTK is widely used in the open-source software community and is the primary toolkit for the GNOME desktop environment. Here are some key aspects of GTK:

1. **Cross-Platform:**
   - GTK is designed to be cross-platform, allowing developers to write applications that run on different operating systems, including Linux, macOS, and Windows.

2. **Widgets:**
   - GTK provides a wide range of user interface elements, known as widgets. These include buttons, text fields, labels, menus, trees, and many more. Developers can use these widgets to create the visual components of their applications.

3. **Event-Driven Programming:**
   - GTK follows an event-driven programming model. Developers define callbacks or handlers for specific events (such as button clicks or key presses), and GTK calls these functions when the corresponding events occur.

4. **Layout Managers:**
   - GTK includes layout managers that help developers organize and position widgets within a window. This allows for the creation of flexible and responsive user interfaces.

5. **Theming:**
   - GTK supports theming, allowing developers to customize the appearance of their applications. Themes control the colors, fonts, and overall look and feel of GTK-based applications.

6. **Internationalization (i18n) and Accessibility:**
   - GTK includes features for internationalization, making it easier to translate applications into different languages. It also supports accessibility features to ensure that applications are usable by people with disabilities.

7. **Integration with Other Libraries:**
   - GTK can be used in conjunction with other libraries and tools. For example, it works well with the GLib library, and applications often use the GObject type system for object-oriented programming.

8. **Open Source and Community-Driven:**
   - GTK is open source, and its development is community-driven. This means that developers from around the world contribute to its improvement, ensuring continuous updates and enhancements.

Overall, GTK provides a powerful and flexible framework for building desktop applications with rich graphical user interfaces, making it a popular choice for software developers working in the Linux and open-source ecosystems.

# Build from Source (for Debian)

## Requirements / Prerequisites 
You need the development package for `gstreamer-player-1.0`. On **Debian** it is provided by `libgstreamer-plugins-bad1.0-dev`

```bash
sudo apt-get update
sudo apt install libgstreamer-plugins-bad1.0-dev
```
On other distros, if above installation fails, try:

```bash
sudo apt-get update
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev

```

# Dependencies

Before you can compile the GTK widget toolkit, you need to have various other tools and libraries installed on your system. Dependencies of GTK have their own build systems, so you will need to refer to their own installation instructions.

A particular important tool used by GTK to find its dependencies is `pkg-config`.

**pkg-config** is a tool for tracking the compilation flags needed for libraries that are used by the GTK libraries. (For each library, a small .pc text file is installed in a standard location that contains the compilation flags needed for that library along with version number information.)

Some of the libraries that GTK depends on are maintained by the GTK team: `GLib, GdkPixbuf, Pango, and GObject Introspection`. Get more informations about them [here](https://docs.gtk.org/).
Other libraries are maintained separately.

- **The GLib library** provides core non-graphical functionality such as high-level data types, Unicode manipulation, and an object and type system to C programs. It is available [here](https://download.gnome.org/sources/glib/).
- **The GdkPixbuf library** provides facilities for loading images in a variety of file formats. It is available [here](https://download.gnome.org/sources/gdk-pixbuf/).
- **Pango** is a library for internationalized text handling. It is available [here](https://docs.gtk.org/Pango/).
- **GObject Introspection** is a framework for making introspection data available to language bindings. It is available [here](https://download.gnome.org/sources/gobject-introspection/).
- **The GNU libiconv library** is needed to build GLib if your system doesn’t have the `iconv()` function for doing conversion between character encodings. Most modern systems should have `iconv()`.
- **The libintl library** from the GNU gettext package is needed if your system doesn’t have the `gettext()` functionality for handling message translation databases.
- **The libraries from the X window system** are needed to build Pango and GTK. You should already have these installed on your system, but it’s possible that you’ll need to install the development environment for these libraries that your operating system vendor provides.
- **The fontconfig library** provides Pango with a standard way of locating fonts and matching them against font names.
- **Cairo** is a graphics library that supports vector graphics and image compositing. Both Pango and GTK use Cairo for drawing. Note that we also need the auxiliary cairo-gobject library. [Download cairo here](https://www.cairographics.org/documentation/).
- **libepoxy** is a library that abstracts the differences between different OpenGL libraries. GTK uses it for cross-platform GL support and for its own drawing.[Download Epoxy here](https://download.gnome.org/sources/libepoxy/)
- **Graphene** is a library that provides vector and matrix types for 2D and 3D transformations. GTK uses it internally for drawing. [Download Graphene here](https://packages.debian.org/source/sid/graphene)
- **The Wayland libraries** are needed to build GTK with the Wayland backend.
- **The shared-mime-info package** is not a hard dependency of GTK, but it contains definitions for mime types that are used by GIO and, indirectly, by GTK. gdk-pixbuf will use GIO for mime type detection if possible. For this to work, shared-mime-info needs to be installed and `XDG_DATA_DIRS` set accordingly at configure time. Otherwise, gdk-pixbuf falls back to its built-in mime type detection.

# Librairies sources downloading for installation

You must download and build librairies int this order : `GLib, Cairo, Pango`,..., then `GTK`.

All the dependencies can be found here so : 
- For GNU Linux/UNIX : [https://www.gtk.org/docs/installations/linux/](https://www.gtk.org/docs/installations/linux/)
- For other, please visit : [https://www.gtk.org/](https://www.gtk.org/) and click on the **Download** button.

## Download GLib sources on official website.
visit [linux from scratch](https://www.linuxfromscratch.org/blfs/view/svn/general/glib2.html) for details about installing from scratch.
```bash
# download source from hhttps://download.gnome.org/sources/glib/
# decompress
tar ~/Downloads/glib-2.9.6.tar.xz
# rename
mv ~/Downloads/glib-2.9.6 ~/Downloads/glib
# copying
sudo mv ~/Downloads/glib/ /opt/glib 
# goto /opt/glib 
cd /opt/glib 
```
All the details for installing glib are in `/opt/glib/INSTALL` file.
Read it : `vim /opt/glib/INSTALL`
```bash
# run the `configure' script
./configure
# build GLIB
make
# [ Become root if necessary ]
sudo rm -rf /install-prefix/include/glib.h /install-prefix/include/gmodule.h
# install GLIB
sudo make install
```

## Installing Cairo.
```bash
sudo apt-get install libcairo2-dev
```
## Download Pango sources on official website.

## Installing gobject-introspection
visit [linux from scratch](https://www.linuxfromscratch.org/blfs/view/svn/general/gobject-introspection.html) for details about installing from scratch.
```bash
# download source from https://download.gnome.org/sources/gobject-introspection/
# decompress
tar ~/Downloads/gobject-introspection-1.79.1.tar.xz
# rename
mv ~/Downloads/gobject-introspection-1.79.1 ~/Downloads/gobject
# copying
sudo mv ~/Downloads/gobject/ /opt/gobject 
# goto /opt/gobject 
cd /opt/gobject 
```
After that, execute :
```bash
# build gobject for our computer for progamming using gobject
mkdir build &&
cd    build &&

meson setup --prefix=/usr --buildtype=release .. &&
ninja
ninja install
```

## Download gtk4 sources on official website.

The downloaded file is in the `~/Downloads` folder of the computer and it looks like : `gtk-4.9.4.tar.xz`

Decompress and rename it before copying the whole renamed folder to `/opt/`.

```bash
# decompress
tar ~/Downloads/gtk-4.9.4.tar.xz
# rename
mv ~/Downloads/gtk-4.9.4 ~/Downloads/gtk
# copying
sudo mv ~/Downloads/gtk/ /opt/gtk 
# goto /opt/gtk 
cd /opt/gtk 
# build gtk for our computer for progamming using gtk
meson setup --prefix /opt/gtk builddir

```
After that, since we are inside our `/opt/gtk` directory, let's execute following lines too:

```bash
cd /opt/gtk/builddir
ninja
ninja install
```
If you don’t have permission to write to the directory you are installing in, **you may have to change to root** temporarily before running `ninja install`.
```bash
cd /opt/gtk/builddir
sudo ninja
sudo ninja install
```
## Useful environment variables

Several environment variables are useful to pass to set before running meson. CPPFLAGS contains options to pass to the C compiler, and is used to tell the compiler where to look for include files. The LDFLAGS variable is used in a similar fashion for the linker. Finally the PKG_CONFIG_PATH environment variable contains a search path that pkg-config (see below) uses when looking for files describing how to compile programs using different libraries. If you were installing GTK and it’s dependencies into /opt/gtk, you might want to set these variables as:

```bash
CPPFLAGS="-I/opt/gtk/include"
LDFLAGS="-L/opt/gtk/lib"
PKG_CONFIG_PATH="/opt/gtk/pkgconfig"
export CPPFLAGS LDFLAGS PKG_CONFIG_PATH
 
LD_LIBRARY_PATH="/opt/gtk/lib"
PATH="/opt/gtk/bin:$PATH"
export LD_LIBRARY_PATH PATH
```
Or let's write in one of these files depending on your OS : `.bashrc` , `.bash_profile`, `.zshrc`.

As I'm using **Debian 12**, mine is `.zshrc`.
Open it and paste following lines inside it: 

```bash
vim ~/.zshrc 
```
paste :

```raw
export CPPFLAGS="-I/opt/gtk/include"
export LDFLAGS="-L/opt/gtk/lib"
export PKG_CONFIG_PATH="/opt/gtk/pkgconfig"

export LD_LIBRARY_PATH="/opt/gtk/lib"
export PATH="/opt/gtk/bin:$PATH"
```
# Removing environement variables

If you want to remove or unset the environment variables `CPPFLAGS`, `LDFLAGS`, and `PKG_CONFIG_PATH` 
that you have set, you can use the unset command in your terminal. Here's how you can do it:

```bash
unset CPPFLAGS LDFLAGS PKG_CONFIG_PATH
```
If you want to remove or unset the environment variables `CPPFLAGS`, `LDFLAGS`, and `PKG_CONFIG_PATH` that you have set, you can use the `unset` command in your terminal. Here's how you can do it:

After running this command, these environment variables will no longer be set in your current shell session.

If you want to ensure that these changes persist across new terminal sessions, you should check the configuration files that are sourced when you start a new shell session. Common configuration files include `.bashrc`, `.bash_profile`, `.zshrc`, or similar, depending on your shell. You can edit the appropriate file and remove or comment out the lines where these environment variables are set.

For example, if you were using Bash, you might open your `.bashrc` file and look for the lines:

```bash
export CPPFLAGS="-I/opt/gtk/include"
export LDFLAGS="-L/opt/gtk/lib"
export PKG_CONFIG_PATH="/opt/gtk/pkgconfig"
```

Remove or comment out these lines by adding a `#` at the beginning:

```bash
# export CPPFLAGS="-I/opt/gtk/include"
# export LDFLAGS="-L/opt/gtk/lib"
# export PKG_CONFIG_PATH="/opt/gtk/pkgconfig"
```
Save the file, and the changes will take effect the next time you start a new shell session.

# TESTING gtk4

After installing all the necessary librairies, you have to test if all things are correct.

Write C program using gtk4 for its GUI:

```c
#include <gtk/gtk.h>

static void
click1_cb (GtkButton *btn) {
  const char *s;

  s = gtk_button_get_label (btn);
  if (g_strcmp0 (s, "Hello.") == 0)
    gtk_button_set_label (btn, "Good-bye.");
  else
    gtk_button_set_label (btn, "Hello.");
}

static void
click2_cb (GtkButton *btn, GtkWindow *win) {
  gtk_window_destroy (win);
}

static void
app_activate (GApplication *app) {
  GtkWidget *win;
  GtkWidget *box;
  GtkWidget *btn1;
  GtkWidget *btn2;

  win = gtk_application_window_new (GTK_APPLICATION (app));
  gtk_window_set_title (GTK_WINDOW (win), "lb4");
  gtk_window_set_default_size (GTK_WINDOW (win), 400, 300);

  box = gtk_box_new (GTK_ORIENTATION_VERTICAL, 5);
  gtk_box_set_homogeneous (GTK_BOX (box), TRUE);
  gtk_window_set_child (GTK_WINDOW (win), box);

  btn1 = gtk_button_new_with_label ("Hello.");
  g_signal_connect (btn1, "clicked", G_CALLBACK (click1_cb), NULL);

  btn2 = gtk_button_new_with_label ("Close");
  g_signal_connect (btn2, "clicked", G_CALLBACK (click2_cb), win);

  gtk_box_append (GTK_BOX (box), btn1);
  gtk_box_append (GTK_BOX (box), btn2);

  gtk_window_present (GTK_WINDOW (win));
}

int
main (int argc, char **argv) {
  GtkApplication *app;
  int stat;

  app = gtk_application_new ("com.github.ToshioCP.lb4", G_APPLICATION_DEFAULT_FLAGS);
  g_signal_connect (app, "activate", G_CALLBACK (app_activate), NULL);
  stat =g_application_run (G_APPLICATION (app), argc, argv);
  g_object_unref (app);
  return stat;
}
```
Aave it under `testgtk4.c` name and compile it:

```bash
# compilation
gcc testgtk4.c $(pkg-config --cflags --libs gtk4) -o program

# Running
./program
```
You must see a window. if yes, it works!

# Sources :

- [learning how to install libraries for Linux from scratch using source](https://www.linuxfromscratch.org/)
- [GStreamer Installation on Linux](https://gstreamer.freedesktop.org/documentation/installing/on-linux.html?gi-language=c)

- [GStreamer Player 1.0 - Not Found](https://discourse.gnome.org/t/gstreamer-player-1-0-not-found-though-gstreamer-is-installed-and-newest-available-version/8879)

- [GStreamer Installation Guide (Thiblahute's Version)](https://thiblahute.github.io/GStreamer-doc/installing/on-linux.html?gi-language=c)

- [Gtk4 Official Website for Downloading](https://www.gtk.org/)

- [Gtk4 Official Documentation](https://docs.gtk.org/gtk4/index.html)

- [Learn Gtk4 with Official Documentation](https://www.gtk.org/docs/)

- [Official Sources Direct Links for Linux/Unix](https://www.gtk.org/docs/installations/linux/)

- [Official Sources Direct Links for Windows](https://www.gtk.org/docs/installations/windows/)

- [Official Sources Direct Links for macOS](https://www.gtk.org/docs/installations/macos/)

