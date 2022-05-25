
Lockpack (or `pack`) is a dead simple generic lockfile spec and tool to manipulate lockpacks.
It utilizes IPFS to make lockpacks (called `pack.jams`) into lightweight package manifests.

A `pack.jams` (or JSON) object can only have values that are `ipfs://` URLs,
or `dmap://` URLs where the dpath contains only locked values.

`pack.jams` describes how to populate files and folders into
a folder called `.pack` which sits next to that `pack.jams` file.

Example pack.jams:

```
{
  tapzero  ipfs://...
  wethpack dmap://:pack:weth
}
```

Then `pack pull` will try to get files from IPFS to make you the following:

```
yourthing/
  .pack/
    tapzero
    wethpack
  pack.jams
```

`pack lock` will save the current version of the directory with
`.pack` removed to local IPFS and show you the CID. From there you
can pin and publish it however you want. If lock the CID into dmap,
you can just publish a dpath.

Note that packages do not self-name or self-version, they are nothing more
than a way to introduce a layer of indirection to IPFS so your toolchain
can manage how deep into the dependency tree it goes in different situations.

