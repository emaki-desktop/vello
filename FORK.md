# Fork notes — vello

A fork of [vello](https://github.com/linebender/vello), Linebender's GPU 2D renderer, kept for
the [amane](https://github.com/emaki-desktop/amane) fork and the
[emaki](https://github.com/emaki-desktop/emaki) desktop. It makes the compute renderer
(`vello`, `vello_encoding`) fit a desktop shell's GPU memory: scratch buffers sized for a
shell's scenes instead of paris-30k, an image atlas that shrinks when its images go, and a buffer
pool that lets go of what no run takes any more. On an integrated GPU that is some 300 MB less
than upstream while the desktop sits idle.

- Branch `emaki`, a short series of commits over upstream `main` at the tag
  `fork-base-2026-11-07` (commit `c161b8ae`, 50 commits after `v0.11.0`). The workspace version
  stays `0.11.x`, so a `vello = "0.11"` dependency takes the fork through `[patch.crates-io]`.
- Footprint: only `research/vello_encoding` and `research/vello_research` change. Upstream's
  files are left as they are, except for the one-line banner at the top of `README.md` that
  points here; `FORK.md`, `docs/fork/` and `.github/workflows/fork.yml` are the fork's own.
- Upstream's `ci.yml` and `web-demo.yml` are disabled in this repository's Actions settings;
  `fork.yml` is the fork's CI.

**Using it:** [docs/fork/README.md § Using the fork](docs/fork/README.md#using-the-fork) — the
three changes, the `[patch.crates-io]` snippet, the Nix `outputHashes` note and the knobs
(`use_upstream_scratch`, `Renderer::release_scratch`, the `debug_layers` feature).

**Maintaining it:** [docs/fork/README.md § Maintaining the fork](docs/fork/README.md#maintaining-the-fork)
— the `upstream` remote, the base tag, the rebase routine, `ocbk-pre-tidy`.

These changes are not proposed upstream. Upstream has moved to the sparse-strips renderers
(`vello_cpu`, `vello_gpu`), where the problem does not arise, and moving amane to `vello_gpu`
retires this fork; nothing here opens pull requests or issues against linebender/vello, in line
with upstream's [AGENTS.md](AGENTS.md) and the
[Linebender LLM contribution policy](https://linebender.org/wiki/llm-policy/).
