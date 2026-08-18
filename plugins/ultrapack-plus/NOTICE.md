# Attribution

This plugin is **not original work**. It is a redistribution of:

> **ultrapack** — https://github.com/btseytlin/ultrapack
> © Boris Tseitlin, licensed under [WTFPL](LICENSE.upstream.txt)

Pinned to upstream commit [`4aea8cf`](https://github.com/btseytlin/ultrapack/commit/4aea8cf6f379fd62893834564d9ae18653aaf407) (`main`, August 2026).

WTFPL permits redistribution and modification without restriction. Attribution is
kept here because the license allowing something is not the same as it being
honest to omit it.

## What differs from upstream

**Nothing yet.** Every `SKILL.md` and agent file in this directory is byte-identical
to upstream at the pinned commit. Verify with:

```bash
diff -r <(git clone -q --depth 1 https://github.com/btseytlin/ultrapack /tmp/up && echo /tmp/up/skills) skills/
```

This plugin exists to pin a known-good set and to give local modifications a home
once there are any. Any future divergence must be listed in this section — an
undocumented fork is how people end up debugging a skill that no longer matches
the docs they're reading.

## What is not included

- `.codex-plugin/`, `.agents/` — upstream packaging for other agent runtimes.
- `.github/workflows/` — upstream's own CI.

Only `skills/` and `agents/` are carried, since that is what the plugin runtime reads.

## Upstream is the better source

If you just want ultrapack, install it from the author directly:

```
/plugin marketplace add btseytlin/ultrapack
/plugin install up@ultrapack
```

That gets you updates as they land. This copy does not track upstream automatically.
