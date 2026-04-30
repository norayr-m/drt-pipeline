# DRT Pipeline — the Bach BWV 847 Pipeline

> This is an amateur engineering project. We are not HPC professionals and make no competitive claims. Errors likely.

A browser demo that runs a composer and a decomposer side-by-side on Bach's C-minor fugue, BWV 847. The forward pass turns the fugue subject into the full polyphonic structure; the backward pass takes the polyphonic structure and recovers the subject and the per-voice transformations. Both run in parallel, visibly.

**[Live demo →](https://norayr-m.github.io/drt-pipeline/)**

## What it does

The screen is split into two panels running on the same audio timeline:

- **Forward pass (composition → decomposition).** The fugue subject enters as a single line; voice by voice, the demo unfolds the full polyphonic texture (subject entries, inversions, augmentations, stretto). You see the encoder building the piece up.
- **Backward pass (decomposition → reconstruction).** The full polyphony enters; the demo decomposes it back into per-voice projections and lines them up with the original subject. You see the decoder taking the piece apart.

Both passes run together so you can see the symmetry: the same operators that build the fugue can take it apart, and the same audio drives both views.

## Why it matters (DRT angle)

This is the **forward/backward symmetry slice**. The framework treats a system as a family of partial observers each with a projection $\Pi_i$ (the per-voice operator), a return operator $C_i$ (the per-voice "complete back to global" operator), and an aggregate $R_t(f) = \sum_i \varphi_i \, C_i(\Pi_i f)$. The fugue is one of the cleanest concrete examples in the wild:

- The subject is the original signal $f$.
- Each voice's transformation (transposition, inversion, augmentation, delay) is a projection $\Pi_i$.
- The contrapuntal rules + voice rejoin to subject form is the return operator $C_i$.
- The full polyphonic fugue is the aggregate $R_t(f)$.

The honest current claim from the v0.1 draft is conditional. Earlier prose around this demo asserted "$\|R(f)\| > \|f\|$" — that exact norm-growth inequality has been retracted. The current claim is weaker and conditional: under four explicit hypotheses and a bounded computational budget, the aggregate exposes structural features not accessible from the original signal alone within the same budget. The fugue is not a proof of that statement; it is a 300-year-old artistic example of the pattern.

## How to run

Single HTML, open in a browser:

```
git clone https://github.com/norayr-m/drt-pipeline.git
open drt-pipeline/index.html
```

No build step. No server. Audio is opt-in.

## Companion work

- **DRT_Decoder_of_the_Encoder** — the same fugue rendered as a navigable graph tree (single-pass, more visualisation-oriented).

## References

- Bach, J. S. — *The Well-Tempered Clavier*, Book I, BWV 847 (1722).
- Distributed Reconstruction work — v0.1 in preparation, N. Matevosyan and A. Petrosyan.

Visualization co-authored with Claude (Anthropic).

## Author

Norayr Matevosyan

## License

GPLv3
