# Piper voices — `high` quality tier (English)

All five English voices Piper publishes at the **`high`** quality tier, mirrored from
[`rhasspy/piper-voices`](https://huggingface.co/rhasspy/piper-voices) on HuggingFace.

`high` is the top tier Piper ships. Upstream has 177 voices total, but only 14 at `high`
(123 are `medium`, 26 `low`, 14 `x_low`) — of those 14, these 5 are the English ones.

All models are 22,050 Hz.

| Voice | Locale | Speakers | Size | Dataset licence |
|---|---|---|---|---|
| `en_GB-cori-high` | en_GB | 1 | 109 MB | Public domain (LibriVox) |
| `en_US-lessac-high` | en_US | 1 | 109 MB | [Blizzard 2013 licence](https://www.cstr.ed.ac.uk/projects/blizzard/2013/lessac_blizzard2013/license.html) |
| `en_US-libritts-high` | en_US | **904** | 130 MB | CC BY 4.0 |
| `en_US-ljspeech-high` | en_US | 1 | 109 MB | Public domain |
| `en_US-ryan-high` | en_US | 1 | 115 MB | **CC BY-NC-SA 4.0 — non-commercial** |

Each voice is three files: the `.onnx` model, its `.onnx.json` config (required — Piper will
not load a model without it), and the upstream `MODEL_CARD`.

## ⚠️ Licensing

The Piper *code* is MIT, but each voice inherits the licence of the dataset it was trained on,
and they are **not** uniform:

- **`en_US-ryan-high` is CC BY-NC-SA 4.0** — non-commercial use only, and share-alike.
  Do not ship it in a commercial product.
- **`en_US-lessac-high`** carries the Blizzard Challenge 2013 licence, which is written for
  research use. Read it before deploying.
- `cori` and `ljspeech` are public domain; `libritts` is CC BY 4.0 (attribution required).

See each `MODEL_CARD` for dataset URLs and training notes.

## Git LFS

The `.onnx` files are stored in **Git LFS**. A plain `git clone` gives you pointer files, not
models. You need `git-lfs` installed:

```sh
brew install git-lfs && git lfs install   # macOS
git clone https://github.com/JHeat89/piper-voices.git
```

If you already cloned without LFS:

```sh
git lfs pull
```

To grab a single voice instead of all 572 MB:

```sh
git lfs pull --include="high/en_US-lessac-high.onnx"
```

## Usage

```sh
echo 'Hello world.' | piper -m high/en_US-lessac-high.onnx -f out.wav
```

`libritts` is multi-speaker — pick one of its 904 speakers with `-s`:

```sh
echo 'Hello world.' | piper -m high/en_US-libritts-high.onnx -s 42 -f out.wav
```

## Verifying

```sh
cd high && shasum -a 256 -c SHA256SUMS
```

## Provenance

Mirrored from `rhasspy/piper-voices` @ `main`, 2026-09-29. Files are byte-identical to
upstream; sizes were checked against the HuggingFace API before commit.
