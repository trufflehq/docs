# Importing other packages

{% embed url="https://youtu.be/YnZWLj7BHao" %}

Truffle packages don’t have a package.json. They’re much more similar to a Deno package, where they rely on URL imports instead.

#### npm.tfl.dev

[npm.tfl.dev](http://npm.tfl.dev) is our self-hosted [esm.sh](http://esm.sh) instance.

#### tfl.dev

_**Note: this isn’t complete accurate until we finish work on OSCAR (a Deno-style package server). Until then we host and serve the files statically from Google Cloud Storage**_

[tfl.dev](http://tfl.dev) works similar to npm.tfl.dev, just focused on Deno-style packages.

#### Best practices

* **Import partial semvers to get the most-recent update and ignore breaking changes**
  * **For unstable** (in-development) NPM and Truffle packages (0.y.z), **import with the major and minor versions**. Eg `import Button from "<https://tfl.dev/@truffle/ui**@0.1**/components/button/button.tag.js>"`
  * **For stable packages** (1.y.z and above), **import just the major**, as long as you trust the developer won’t implement breaking changes in a minor release. Eg. `import qs from "<https://npm.tfl.dev/qs**@6**>"`
  * This will help consolidate the number of packages being imported
    * Instead of importing qs@6.10.1, qs@6.7.2 and qs@6.6.0 if multiple packages rely on it and import the full semver, we only import qs@6.11.0 (latest)
