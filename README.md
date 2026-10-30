# ailia JS Package

!! CAUTION !!
“ailia” IS NOT OPEN SOURCE SOFTWARE (OSS).
As long as user complies with the conditions stated in [License Document](https://ailia.ai/license/), user may use the Software for free of charge, but the Software is basically paid software.

## API specification

https://github.com/ailia-ai/ailia-sdk

## WASM variants

`ailia.js` picks the fastest WASM build supported by the environment. The selected one is
exposed as `Ailia.variant` after `Ailia.initialize()`.

| Variant | WASM SIMD | Multithreading |
| --- | --- | --- |
| `ailia_simd_thread_s` | yes | yes |
| `ailia_simd_s` | yes | no |
| `ailia_s` | no | no |

## Enabling multithreading

The multithreaded variant uses `SharedArrayBuffer`, which browsers only expose to
cross-origin isolated pages. To let `ailia.js` select it, the server delivering your page
must send these response headers:

```
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Embedder-Policy: require-corp
```

Without them `ailia.js` transparently falls back to `ailia_simd_s`, so nothing breaks —
inference just runs single-threaded. On Node no extra setup is needed.