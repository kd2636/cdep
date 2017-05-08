# CDep Package Author's Guide
This guide will show how to author your own CDep package and host it on github. When you're done you'll have a package that any CDep user can reference in their project.

## Anatomy of a CDep Package
A CDep package is a manifest file called cdep-manifest.yml along with zipped source and compiled libraries. You can see an example of [here](https://github.com/jomof/re2/releases/download/17.3.1-rev18/cdep-manifest.yml). Here's a fragment of cdep-manifest.yml.
```
coordinate:
  groupId: com.github.jomof
  artifactId: re2
  version: 17.3.1-rev18
license:
  name: "BSD 3-Clause"
  url: "https://raw.githubusercontent.com/google/re2/master/LICENSE"
interfaces:
  headers:
    file: re2-headers.zip
    sha256: 773c6c106e68e1494b8b73f46db4e98dfda901a18c2fbcc5ec762f9f27b94094
    size: 43964
    include: include
    requires: [cxx_deleted_functions, cxx_variadic_templates]
android:
  archives:
  - file: re2-android-21-armeabi.zip
    sha256: 162e6fbe36b1b097c815a629d7c94492b491cf68f8cb2d079c6c97e23fd9785d
    size: 3063095
    platform: 21
    abi: armeabi
    libs: [libre2.a]
  - file: re2-android-21-armeabi-v7a.zip
    sha256: 18e88a1c4e4450346f04d20315a4b251e1181cba7424178a4bd975673658f942
    size: 3027841
    platform: 21
    abi: armeabi-v7a
    libs: [libre2.a]
```

