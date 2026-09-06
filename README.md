# containers

Container images built for the [thaum.xyz](https://github.com/thaum-xyz) cluster
and published to `ghcr.io/thaum-xyz/containers/<name>`.

Split out of [ankhmorpork][a] so image builds and releases have their own CI, not
because the images have an audience of their own. The cluster documentation lives
at [docs.thaum.xyz][docs]; what belongs *here* is whatever a change to a
`Dockerfile` would invalidate.

[a]: https://github.com/thaum-xyz/ankhmorpork
[docs]: https://docs.thaum.xyz/

## Images

| Image | Purpose |
| --- | --- |
| `lvm-tools` | Debian with `lvm2` and `util-linux`, for privileged node disk preparation. Deliberately generic — it ships no script, and the caller supplies the command. |

Which charts and components pull these is recorded in the
[cluster documentation][docs] instead, where a change to the cluster is what
invalidates it.

## Adding an image

Create `images/<name>/Dockerfile`. The release workflow discovers it
automatically — there is no registration step.

## Releases

Pushing to `main` builds every image whose directory changed and tags it
`YYYY.WW.PATCH` — ISO year and week, with the patch number incremented from the
tags already in GHCR.

There is no `latest` tag, so nothing can float onto a new build by accident: a
consumer pins an exact tag, and a new image reaches it only when that pin is
changed.
