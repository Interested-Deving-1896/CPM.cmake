[update-readmes]   Mode: rewrite — migrating to template structure...
# CPM.cmake

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/CPM.cmake)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/CPM.cmake.git
cd CPM.cmake
```

## Usage


After `CPM.cmake` has been [added](#adding-cpm) to your project, the function `CPMAddPackage` can be used to fetch and configure a dependency.
Afterwards, any targets defined in the dependency can be used directly.
`CPMAddPackage` takes the following named parameters.

```cmake
CPMAddPackage(
  NAME          # The unique name of the dependency (should be the exported target's name)
  VERSION       # The minimum version of the dependency (optional, defaults to 0)
  PATCHES       # Patch files to be applied sequentially using patch and PATCH_OPTIONS (optional)
  OPTIONS       # Configuration options passed to the dependency (optional)
  DOWNLOAD_ONLY # If set, the project is downloaded, but not configured (optional)
  [...]         # Origin parameters forwarded to FetchContent_Declare, see below
)
```

The origin may be specified by a `GIT_REPOSITORY`, but other sources, such as direct URLs, are [also supported](https://cmake.org/cmake/help/v3.11/module/ExternalProject.html#external-project-definition).
If `GIT_TAG` hasn't been explicitly specified it defaults to `v(VERSION)`, a common convention for git projects.
On the other hand, if `VERSION` hasn't been explicitly specified, CPM can automatically identify the version from the git tag in some common cases.
`GIT_TAG` can also be set to a specific commit or a branch name such as `master`, however this isn't recommended, as such packages will only be updated when the cache is cleared.

`PATCHES` takes a list of patch files to apply sequentially. For a basic example, see [Highway](examples/highway/CMakeLists.txt).
We recommend that if you use `PATCHES`, you also set `CPM_SOURCE_CACHE`. See [issue 577](https://github.com/cpm-cmake/CPM.cmake/issues/577).

If an additional optional parameter `EXCLUDE_FROM_ALL` is set to a truthy value, then any targets defined inside the dependency won't be built by default. See the [CMake docs](https://cmake.org/cmake/help/latest/prop_tgt/EXCLUDE_FROM_ALL.html) for details.

If an additional optional parameter `SYSTEM` is set to a truthy value, the SYSTEM directory property of the subdirectory added will be set to true.
See the [add_subdirectory ](https://cmake.org/cmake/help/latest/command/add_subdirectory.html?highlight=add_subdirectory)
and [SYSTEM](https://cmake.org/cmake/help/latest/prop_tgt/SYSTEM.html#prop_tgt:SYSTEM) target property for details.

A shorthand syntax is also supported:

```cmake
# A git package from a given uri with a version
CPMAddPackage("uri@version")
# A git package from a given uri with a git tag or commit hash
CPMAddPackage("uri#tag")
# A git package with both version and tag provided
CPMAddPackage("uri@version#tag")
```

In the shorthand syntax if the URI is of the form `gh:user/name`, it is interpreted as GitHub URI and converted to `https://github.com/user/name.git`. If the URI is of the form `gl:user/name`, it is interpreted as a [GitLab](https://gitlab.com/explore/) URI and converted to `https://gitlab.com/user/name.git`. If the URI is of the form `bb:user/name`, it is interpreted as a [Bitbucket](https://bitbucket.org/) URI and converted to `https://bitbucket.org/user/name.git`. Otherwise the URI used verbatim as a git URL. All packages added using the shorthand syntax will be added using the [EXCLUDE_FROM_ALL](https://cmake.org/cmake/help/latest/prop_tgt/EXCLUDE_FROM_ALL.html) and [SYSTEM](https://cmake.org/cmake/help/latest/prop_tgt/SYSTEM.html#prop_tgt:SYSTEM) flag.

The single-argument syntax also works for URLs:

```cmake
# An archive package from a given url. The version is inferred
CPMAddPackage("https://example.com/my-package-1.2.3.zip")
# An archive package from a given url with an MD5 hash provided
CPMAddPackage("https://example.com/my-package-1.2.3.zip#MD5=68e20f674a48be38d60e129f600faf7d")
# An archive package from a given url. The version is explicitly given
CPMAddPackage("https://example.com/my-package.zip@1.2.3")
```

Additionally, if needed, extra arguments can be provided while using single argument syntax by using the shorthand syntax with the `URI` specifier.

```cmake
CPMAddPackage(
  URI "gh:nlohmann/json@3.9.1"
  OPTIONS "JSON_BuildTests OFF"
)
```

The `URI` argument must be the first argument to `CPMAddPackage`.
`URI` automatically sets `EXCLUDE_FROM_ALL YES` and `SYSTEM YES`.
If this is not desired, `EXCLUDE_FROM_ALL NO` and `SYSTEM NO` can be set afterwards.

After calling `CPMAddPackage`, the following variables are defined in the local scope, where `<dependency>` is the name of the dependency.

- `<dependency>_SOURCE_DIR` is the path to the source of the dependency.
- `<dependency>_BINARY_DIR` is the path to the build directory of the dependency.
- `<dependency>_ADDED` is set to `YES` if the dependency has not been added before, otherwise it is set to `NO`.
- `CPM_LAST_PACKAGE_NAME` is set to the determined name of the last added dependency (equivalent to `<dependency>`).

For using CPM.cmake projects with external package managers, such as conan or vcpkg, setting the variable [`CPM_USE_LOCAL_PACKAGES`](#options) will make CPM.cmake try to add a package through `find_package` first, and add it from source if it doesn't succeed.

In rare cases, this behaviour may be desirable by default. The function `CPMFindPackage` will try to find a local dependency via CMake's `find_package` and fallback to `CPMAddPackage`, if the dependency is not found.

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/CPM.cmake`](https://github.com/Interested-Deving-1896/CPM.cmake) and mirrored through:

```
Interested-Deving-1896/CPM.cmake  ──►  OpenOS-Project-OSP/CPM.cmake  ──►  OpenOS-Project-Ecosystem-OOC/CPM.cmake
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
[MIT](https://github.com/Interested-Deving-1896/CPM.cmake/blob/master/LICENSE) © 2026 [Interested-Deving-1896](https://github.com/Interested-Deving-1896)
<!-- AI:end:license -->
