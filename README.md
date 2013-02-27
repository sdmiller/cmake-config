cmake-config
============

Command line tool for getting information about CMake-installed packages, in the vein of pkg-config. 

Build systems are a wonderful thing. Unfortunately, there are more than one. And while CMake is my build system 
of choice for personal research code, I often find myself working within other systems (autoconf, ROS, someone else's 
hard-coded Makefile, etc). Getting these to play nicely with other dependencies can be a pain. 
For packages installed through apt-get, pkg-config lets us query for build information straight from the command line. 
cmake-config attempts to do the same for CMake projects.

Example usage:

```bash
$ cmake-config OpenRAVE
-I/usr/include/openrave-0.8 -L/usr/lib -lopenrave0.8
$ cmake-config --libs-only-l OpenRAVE
-lopenrave0.8
$ cmake-config OpenRAVE --libs-only-L
-L/usr/lib
$ cmake-config OpenRAVE --cflags-only-I
-I/usr/include/openrave-0.8
```

The version can be forced with a --version flag

```bash
$ cmake-config OpenRAVE --version 0.9

$ cmake-config OpenRAVE --version 0.8
-I/usr/include/openrave-0.8 -L/usr/lib -lopenrave0.8
```

If you have a local install, it can be used with the --module-path option

```bash
$ cmake-config PCL --module-path=path/to/pcl/share
```

If you are using a library with components (e.g. Boost), specific components can be specified with the --components option

```bash
$ cmake-config Boost --components thread filesystem
-I/usr/include -L/usr/lib -l/usr/lib/libboost\_thread-mt.so -lpthread -l/usr/lib/libboost\_filesystem-mt.so
```

For a complete list of options, see

```bash
$ cmake-config --help
```

Check out the grossly hacked CMakeLists.txt file (which is also hard-coded into the python script for standalone functionality) to see 
how this is working. Want more features? Let me know or contribute them yourself!
