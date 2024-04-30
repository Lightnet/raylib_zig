# raylib_zig

# Zig:
 * 0.12.0

# raylib:
 * https://github.com/raysan5/raylib/archive/b03c8ba945a06ed1ec3d6ed7c3185e1264909323.tar.gz
 * v5.0 broken from zig and raylib

# Information:
There are two way to install raylib on Zig program langauge.

One using the build.zig.zon dependencies and other manual config path folder.

Note Zig is unstable. It subject to change. As well raylib. As there were some change to reflect the new update of zig.

Zig 0.11.0 have simple package manager. It use url package from build.zig.zon it required some config and checks.

Manage to get it working.  Zig 0.12.0 and raylib 5.0 + master branch.

Note this zig default setup.
```
zig init
```
Note some Zig command have changed.
```
zig init-exe
```
This does not exist. By default it add exe and lib at the same time.

# install guide:

```
scoop install zig
scoop install zls
```

```
zig build run
```
command to build and run application.

It would display window with the message.


# Works:
 - https://puddleofcode.com/story/zig-can-you-c/


## build.zig.zon:

Go to https://github.com/raysan5/raylib for copy link. Where you select download zip.

```
https://github.com/raysan5/raylib/archive/refs/heads/master.zip
```
Replace the ext.
```
https://github.com/raysan5/raylib/archive/refs/heads/master.tar.gz
```
It can done the same with commits. Just replace with the ext for zig to use as dependencies. Note it required build.zig root to see as package.

Add raylib dependencies
```zig
.dependencies = .{
  .raylib = .{
    .url = "https://github.com/raysan5/raylib/archive/b03c8ba945a06ed1ec3d6ed7c3185e1264909323.tar.gz", //master
  },
},
```
zig build

It will give error result return hash check.
```
.hash = "1220b6b6198344837d51588b1ed3f63cd6b56b2d60da675219f7578018b54f885830",
```
Added to the raylib.

build.zig.zon
```zig
.dependencies = .{
  .raylib = .{
      .url = "https://github.com/raysan5/raylib/archive/b03c8ba945a06ed1ec3d6ed7c3185e1264909323.tar.gz", //master
      .hash = "1220b6b6198344837d51588b1ed3f63cd6b56b2d60da675219f7578018b54f885830", //return when using just url.
  },
  //...
```

```
zig build
```
  If there no error then you done. Next is config build.zig.

build.zig
```zig
//...
const optimize = b.standardOptimizeOption(.{});
//...
b.installArtifact(lib);
//...
const raylib = b.dependency("raylib", .{
  .target = target,
  .optimize = optimize,
});
//...
// const exe = b.addExecutable(.{
//...
exe.installLibraryHeaders(raylib.artifact("raylib"));
exe.linkLibrary(raylib.artifact("raylib"));
//...
```
Note they place in order some where as well variable exist on create after.


# refs:
 - https://github.com/enndubyu/scoop-zig
 - https://zig.news/liyu1981/tip-use-any-git-branch-in-buildzigzon-5c3o
 - https://siddharthroy.com/posts/how-to-use-raylib-with-zig-without-any-bindings
 - https://github.com/raysan5/raylib/archive/b03c8ba945a06ed1ec3d6ed7c3185e1264909323.zip
 - https://puddleofcode.com/story/zig-can-you-c/
```
 - zig fetch --save https://github.com/raysan5/raylib/archive/b03c8ba945a06ed1ec3d6ed7c3185e1264909323.tar.gz
```