# Minimal libraries

Small PyTorch libraries for computational imaging. Each one does a single task, lives in its own repository and is written to be read.

## Why

Scientific code often lives inside large frameworks, where the part one needs is hard to read and hard to check in isolation. The libraries collected here are short on purpose. Each does one task in a few hundred lines of implementation, a thousand for the largest; its README states what is computed as formulas, its tests pin every convention against explicit sums, and its notebooks show the computation on examples. The reader in mind is a person who wants to understand an algorithm, check it, adapt it, or copy one file into a project. That a language model can also hold a whole library in its context is a bonus.

Each library

1. has one purpose, stated in one sentence;
2. is written to be read: every non-trivial algorithm comes twice, first as `<name>_plain`, the same algorithm written plainly with loops and no tricks, then as the fast version, and a test holds the two together (a library whose functions are already their formulas has none);
3. depends on PyTorch and little else, acts on trailing axes and leaves leading axes alone as batch, runs on any device, is differentiable, never modifies its input and keeps the precision it was given;
4. states its conventions (signs, normalisations, axes, where the origin sits) and tests them against explicit float64 references;
5. comes with three tutorial notebooks, committed with their outputs: why the library exists, what it computes, a benchmark;
6. stands alone: its own repository, a plain `pip install`, `pytest`, MIT.

Some libraries are extracted from research code, the `ciel` computational-imaging library and [psf_generator](https://github.com/Biomedical-Imaging-Group/psf_generator) at EPFL; the others were written for this collection. The last section of every README is a manifest: purpose, dependencies, size, origin, provenance (how the code was written and who checked it), version and license.

## Two tiers

A minimal library (`minimal-<name>`) does one focused task. It reads top to bottom: the plain version of an algorithm first, the fast version after, the tests pinning the two together, three tutorial notebooks.

An essential library (`essential-<name>`) treats one topic completely, on top of the minimal libraries it declares as dependencies. A small package holds the shared pieces (forward models, constraints, metrics, the algorithms of the topic); the substance is a numbered series of notebooks, one chapter each, that reads like an encyclopedia entry with running code.

## Catalogue

| Library | Purpose |
|---|---|
| [minimal-zoom-fft](https://github.com/jon-dong/minimal-zoom-fft) | Zoomed FFT by the chirp Z-transform: the spectrum on any band, at any sampling, N-D, with its adjoint. |
| [minimal-linop](https://github.com/jon-dong/minimal-linop) | Linear operators with exact adjoints, composable with `@`, `+`, `*` and `.H`: FFT, masks, crops, shifts, patches, gradients, resampling. |

In preparation, to be published one by one as each is reviewed: Zernike polynomials, phase unwrapping, free-space propagation, the non-uniform FFT, the orthogonal wavelet transform, the Radon transform, subpixel shifts and registration, multislice propagation, coherent demodulation, conjugate gradients and LSQR, ISTA and FISTA, the leading eigenpair of a Hermitian operator, proximal operators, Wiener and Richardson-Lucy deconvolution, Fisher information and the Cramér-Rao bound, Fourier ring correlation, and an essential library on phase retrieval.

## Install

Each library installs on its own, from its repository:

```bash
pip install git+https://github.com/jon-dong/minimal-zoom-fft
```

They are on PyPI under the same names, `pip install minimal-zoom-fft`. They require Python 3.10 or later and PyTorch 2.0 or later, and nothing else. The one link between them so far: `minimal-linop` has an optional `fft` extra that brings in `minimal-zoom-fft` for one operator.

## Anatomy of a library

```text
minimal-<name>/
├── README.md               purpose, install, quick start, API, conventions, tutorials, tests, manifest
├── LICENSE                 MIT
├── pyproject.toml          name, version, dependency on torch; `test` and `notebooks` extras
├── .github/workflows/      the tests on every push; publication on a version tag
├── src/minimal_<name>/     the implementation, plain versions first
├── notebooks/              01 why, 02 what it computes, 03 benchmark
└── tests/                  pytest; the README examples and the notebooks run as tests
```

The README states the definitions as formulas, and its Python examples are executed by the test suite, so they stay true. The tests compare against explicit float64 summation, against `torch` or `scipy` where a special case exists, and check adjoints with the dot-product test. The notebooks need the `notebooks` extra (numpy, scipy, matplotlib, jupyter), which the library itself never imports.

## License

MIT, stated in each repository.

Jonathan Dong, EPFL.
