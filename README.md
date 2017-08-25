[![Build Status](https://travis-ci.org/google/cdep.svg?branch=master)](https://travis-ci.org/google/cdep)
[![Gitter](https://badges.gitter.im/google-cdep/Lobby.svg)](https://gitter.im/google-cdep/Lobby)

# CDep
CDep is a decentralized native package dependency manager with a focus on Android. 
- Runs on Windows, Linux, and MacOS 
- Works with [Android Studio](https://d.android.com/studio/index.html), CMake, and [ndk-build](https://d.android.com/ndk/guides/ndk-build.html). CMake support is for both [Android Studio version of CMake](https://developer.android.com/studio/projects/add-native-code.html) and the built-in Android support that was added to CMake in version 3.7.1.

Anyone can author a package and there is a growing list of useful packages, such as [Freetype 2.0](https://github.com/jomof/freetype), [SDL](https://github.com/jomof/sdl), [ShaderC](https://github.com/ggfan/shaderc/releases), [STB](https://github.com/jomof/stb), [RE2 Regular Expressions](https://github.com/jomof/re2), [Firebase](https://github.com/jomof/firebase), [MathFu](https://github.com/jomof/mathfu), [Vectorial](https://github.com/jomof/vectorial), [Boost](https://github.com/jomof/boost), [Yaml-CPP](https://github.com/jomof/yaml-cpp), [SQLite](https://github.com/jomof/sqlite), [LUA](https://github.com/jomof/lua).
   
CDep comes from members of the Android Studio team and is not an official Google product. It is a work in progress and subject to change over time. Backward compatibility with existing packages will be maintained.
   
## Get started with CDep
Here are some things you can do to get started with CDep.
* [Add CDep dependencies to an existing Android Studio CMake project](doc/android-studio-cmake.md)
* [Author a negfd\ and SDL2 sample](https://github.com/jomof/cdep-android-studio-freetype-sample)
* [See an Android Studio ndk-build sample](https://github.com/jomof/ndk-build-meet-cdep)
* [Learn how CDep resolves coordinates](doc/coordinate-resolution.md)
* [Learn about CDep tool command line flags](doc/command-line-flags.md)
* [Learn about cdep.yml file](doc/cdep-yml.md)

## Getting started on Windows
Get started with CDep on Windows, enter the f

After this, the instructions are the same as Linux and Mac.

## Getting started on Linux and Mac
Get started with CDep on Linux or Mac by following these steps:
1. Open a terminal window and navigate to the direcotry where your project is located.
2. Enter the following commands: 
     ```
     $ git clone https://github.com/jomof/cdep-redist.git  
     $ cd my-project
     $ ../cdep-redist/cdep wrapper
     ```
   This creates the following files in your local directory (and are meant to be checked into source control):
   ```
   cdep   
   cdep.bat
   cdep.yml
   bootstrap\wrapper\bootstrap.jar
   ```
3. Open `cdep.yml` and add the following line:
   ```
   dependencies:
   # This line tells CDep that your project depends on SQLite.
   - compile: com.github.jomof:sqlite:3.16.2-rev51
   ```
   Learn more about the cdep.yml file [here](doc/cdep-yml.md).
4. Run the `cdep` command to download SQLite and generate CMake module for it.
    ```
    $ ./cdep
    Generating .cdep/modules/cdep-dependencies-config.cmake
    ```   
5. If you have a CMake project, open your `CMakeLists.txt` and add the following code at the end of the file. This tells CMake to locate the module glue file and add all the dependencies in that file to `your_target_library`.
   ```
   find_package(cdep-dependencies REQUIRED)
   add_all_cdep_dependencies(your_target_library)
   ```
   When you call CMake to generate the project you'll need to tell it where to find the glue modules. So something like,
   ```
   cmake -Dcdep-dependencies_DIR=.cdep/modules
   ```
For more details on setting up CMake build with CDep visit [Add CDep dependencies to an existing Android Studio CMake project](https://github.com/google/cdep/blob/master/doc/android-studio-cmake.md).
