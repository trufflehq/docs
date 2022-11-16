# Importing code (eg npm)

{% embed url="https://youtu.be/YnZWLj7BHao" %}

Truffle packages don’t have a package.json. They’re much more similar to a Deno package, where they rely on URL imports instead.

#### npm.tfl.dev

[npm.tfl.dev](http://npm.tfl.dev) is our self-hosted [esm.sh](http://esm.sh) instance.

#### tfl.dev

[tfl.dev](http://tfl.dev) works similar to npm.tfl.dev, just focused on Deno-style packages ([see Oscar](https://github.com/trufflehq/oscar)). You'll notice all of our packages (eg @truffle/api) are hosted on tfl.dev.&#x20;

#### Best practices

* **Import partial semvers to get the most-recent update and ignore breaking changes**
  * **For unstable** (in-development) packages (0.y.z), use `~` so it'll use the latest patch version
    * `import { useStyleSheet } from "https://tfl.dev/@truffle/distribute@^2.0.0/format/wc/react/index.ts"`
  * **For stable packages** (1.y.z and above), **import just the major**, as long as you trust the developer won’t implement breaking changes in a minor release, use `^` so it'll use the latest patch **or** minor version
    * `import { gql, useQuery } from 'https://tfl.dev/@truffle/api@~0.1.15/client.ts'`
