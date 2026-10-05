# Minimal libraries

Small PyTorch libraries for computational imaging. One task each, short enough to read
whole, each in its own repository.

Most scientific code sits inside a framework, where the part you need is hard to find
and harder to check. Here a library is a few hundred lines: formulas in the README,
tests that pin every convention, three notebooks. Every non-trivial algorithm comes
twice, a plain version with loops and a fast one, held equal by a test. Trailing axes
are the signal, leading axes are batch; any device, differentiable, dtype preserved.

## Libraries

| Library | Purpose |
|---|---|
| [minimal-zoom-fft](https://github.com/jon-dong/minimal-zoom-fft) | Zoomed FFT by the chirp Z-transform, with its adjoint. |
| [minimal-linop](https://github.com/jon-dong/minimal-linop) | Linear operators with exact adjoints, composable with `@`, `+`, `*` and `.H`. |

More are on the way, one at a time as each is reviewed.

## Install

```bash
pip install git+https://github.com/jon-dong/minimal-zoom-fft
pip install git+https://github.com/jon-dong/minimal-linop
```

Python 3.10 or later, PyTorch 2.0 or later, nothing else. `minimal-linop` has an
optional `fft` extra that brings in `minimal-zoom-fft` for one operator.

## Layout

```text
minimal-<name>/
├── README.md               purpose, install, quick start, API, conventions, manifest
├── pyproject.toml          version, torch; `test` and `notebooks` extras
├── .github/workflows/      tests on every push, PyPI on a version tag
├── src/minimal_<name>/     the implementation, plain versions first
├── notebooks/              01 why, 02 what it computes, 03 benchmark
└── tests/                  pytest; the README and the notebooks run as tests
```

The last section of each README is a manifest: purpose, dependencies, size, origin,
provenance, version and license.

## License

MIT. Jonathan Dong, EPFL.
