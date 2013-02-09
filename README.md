cmake-config
============

Command line tool for getting information about CMake-installed packages, in the vein of pkg-config. 

Build systems are a wonderful thing. Unfortunately, there are more than one. And while CMake is my build system 
of choice for personal research code, I often find myself working with other systems (autoconf, ROS, someone else's 
hard-coded Makefile, etc). For packages installed through apt-get, pkg-config lets us query for build information. 
cmake-config attempts to do the same for CMake projects.

This is, admittedly, a total hack -- it creates a CMakeLists.txt, configures while printing out useful variables, and 
scrapes out the important information. The naming conventions are meant to follow the similar pkg-config. 

Example usage:

$ cmake-config OpenRAVE
-I/usr/include/openrave-0.8 -L/usr/lib -lopenrave0.8
$ cmake-config --libs-only-l OpenRAVE
-lopenrave0.8

The version can be forced with a --version flag
$ cmake-config OpenRAVE --version 0.9

$ cmake-config OpenRAVE --version 0.8
-I/usr/include/openrave-0.8 -L/usr/lib -lopenrave0.8

If you have a local install, it can be used with the --module-path option
$ cmake-config PCL --module-path=path/to/pcl/share

If you are using a library with components (e.g. Boost), specific components can be specified with the --components option
$ cmake-config Boost --components thread filesystem
-I/usr/include -L/usr/lib -l/usr/lib/libboost\_thread-mt.so -lpthread -l/usr/lib/libboost\_filesystem-mt.so

Check out the CMakeLists.txt file (which is also hard-coded into the python script for standalone functionality) to see 
how this is working. Want more features? Let me know or contribute them yourself!
