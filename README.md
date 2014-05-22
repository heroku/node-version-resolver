# node-version-resolver

> Give me a semver range and I'll tell you the latest node version that
> satisfies it.

node-version-resolver is a node module that can be use programatically or from
the command line. It downloads a list of all Node.js versions from
[nodejs.org/dist](http://nodejs.org/dist) and exposes a simple API for
selecting the latest stable (and unstable) versions, as well as matching the
version list against a [semver
range](https://npmjs.org/doc/misc/semver.html#Ranges).

node-version-resolver's functionality is also available as an HTTP webservice
at [semver.io](https://semver.io).

**Note**: `0.8.6` is the oldest available version of node returned by this library.
This choice was made because nodejs.org does not provide builds of older
versions.

## Installation

```
npm install node-version-resolver --save
```

## Command-Line Usage

Pass a [semver range](https://npmjs.org/doc/misc/semver.html#Ranges) argument
to find what version of Node.js currently satisfies it:

```sh
node-version-resolver 0.10.x
# 0.10.22
```

Or omit the argument to get the latest stable version:

```sh
node-version-resolver
# 0.10.22
```

## Programmatic Usage

See `test/indexText.coffee`

## Caching

node-version-resolver is designed to work even if nodejs.org is down or slow
to respond. If the GET request to [nodejs.org/dist/](http://nodejs.org/dist/)
takes too long to resolve, a local copy of `cache/node.html` file will be
loaded instead. To update the cached file, run:

```
npm run updateCache
```

## Tests

```
npm test

initialization
  ✓ has an array of all versions
  ✓ has an array of stable versions
  ✓ has a latest_stable version
  ✓ has a latest_unstable version
  ✓ defaults to latest stable version when given crazy input
satisfy()
  ✓ honors explicit version strings
  ✓ matches common patterns to stable version
  ✓ uses latest unstable version when request version is beyond stable version
override
  ✓ becomes latest_stable
  ✓ satisfies stable-seeking ranges
  ✓ still resolves unstable ranges
  ✓ still resolves versions at a higher patchlevel than the override
```
