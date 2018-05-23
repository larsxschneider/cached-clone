# Cached Clone

Clone a repository and leverage a local cache. Git submodules and Git LFS files are cached as well.

## Install

Copy `git-cclone` to a directory in your path.

## Usage

```
git cclone <repo-url> <cache-dir> <working-copy-dir> <ref>
```

- `repo-url` is the URL of the repository you want to clone
- `cache-dir` is the directory used for caching (can grow large!)
- `working-copy-dir` is the directory for the checkout (is always purged!)
- `ref` is the branch you want to checkout (can also be a pull request ref such as `pull/<pr-id>/head` or `pull/<pr-id>/merge`)

## Example Usage

The first run populates the cache and clones (takes 36 seconds in this example):
```
$ git cclone https://github.com/git/git cache repo master

>>> Cached Clone v0.0.2
Start date:   Wed May 22 23:24:25 CEST 2018
Cache:        /tmp/cache
Working Copy: /tmp/repo
git version 2.17.0
git-lfs/2.3.4 (GitHub; darwin amd64; go 1.9.1)

>>> Initializing Cache

>>> Updating Cache
remote: Counting objects: 236782, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 236782 (delta 11), reused 10 (delta 10), pack-reused 236769
Receiving objects: 100% (236782/236782), 84.31 MiB | 4.82 MiB/s, done.
Resolving deltas: 100% (176108/176108), done.
From https://github.com/git/git
 * [new branch]          master     -> 7e658b306f7ef364b131937fd476976f2301cbcd/heads/master
Fetching e144d126d74f5d2702870ca9423743102eec6fcd

>>> Preparing Checkout

>>> Updating Cache (Submodule 'sha1collisiondetection')
warning: no common commits
remote: Counting objects: 864, done.
remote: Total 864 (delta 0), reused 0 (delta 0), pack-reused 864
Receiving objects: 100% (864/864), 601.99 KiB | 1.08 MiB/s, done.
Resolving deltas: 100% (560/560), done.
From https://github.com/cr-marcstevens/sha1collisiondetection
 * [new branch]          master     -> 67f25e12b4ab7f4f9da1e5dc0a41a5ab66108279/heads/master
 * [new branch]          simd       -> 67f25e12b4ab7f4f9da1e5dc0a41a5ab66108279/heads/simd
Fetching 19d97bf5af05312267c2e874ee6bcf584d9e9681

>>> Preparing Checkout (Submodule 'sha1collisiondetection')

>>> Runtime (sec): 36

>>> Success!
```


Any subsequent run only updates the cache and clones (takes 4 seconds in this example):
```
$ git cclone https://github.com/git/git cache repo master

>>> Cached Clone v0.0.2
Start date:   Wed May 22 23:30:00 CEST 2018
Cache:        /tmp/cache
Working Copy: /tmp/repo
git version 2.17.0
git-lfs/2.3.4 (GitHub; darwin amd64; go 1.9.1)

>>> Updating Cache
Fetching e144d126d74f5d2702870ca9423743102eec6fcd

>>> Preparing Checkout

>>> Updating Cache (Submodule 'sha1collisiondetection')
Fetching 19d97bf5af05312267c2e874ee6bcf584d9e9681

>>> Preparing Checkout (Submodule 'sha1collisiondetection')

>>> Runtime (sec): 4

>>> Success!
```


## License

SPDX-License-Identifier: [MIT](LICENSE.md)
