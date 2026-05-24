# THIRD_PARTY_NOTICES

This file collects third-party libraries, references, and acknowledgements used or referenced by **Mandel Zoom Abyss**.

このファイルは、**Mandel Zoom Abyss** で利用・参照している外部ライブラリ、参考作品、謝辞をまとめたものです。  
正確なライセンス条件については、各プロジェクトの公式ページ・リポジトリ・配布物に含まれるライセンス文を確認してください。

---

## gmp-wasm

- Project: gmp-wasm
- Repository: https://github.com/Daninet/gmp-wasm
- npm: https://www.npmjs.com/package/gmp-wasm
- License: LGPL-3.0
- Author / Maintainer: Daninet and contributors

Mandel Zoom Abyss loads `gmp-wasm` from jsDelivr and uses it for high-precision CPU-side reference orbit calculation.

This project uses the high-level JavaScript/WebAssembly wrapper provided by `gmp-wasm`.  
The underlying arbitrary-precision integer, rational, and floating-point operations are based on GMP and MPFR.

本作品では、CPU側で高精度な基準軌道を計算するために `gmp-wasm` を利用しています。  
ブラウザ上でGMP/MPFRベースの多倍長計算を扱えるようにしてくれている、とてもありがたいライブラリです。

---

## GMP - GNU Multiple Precision Arithmetic Library

- Project: GMP - GNU Multiple Precision Arithmetic Library
- Website: https://gmplib.org/
- License: GNU LGPL v3 and GNU GPL v2 dual license

GMP is used indirectly through `gmp-wasm`.

In Mandel Zoom Abyss, GMP-based high-precision arithmetic is used to compute the reference orbit on the CPU side.  
The live WebGPU shader then renders nearby pixels as f32 perturbations from that reference orbit.

本作品では、GMPを直接ビルド・同梱しているのではなく、`gmp-wasm` 経由で利用しています。  
GMPによる多倍長計算があることで、通常のfloat64だけでは難しい深いズームの基準軌道を維持できます。

---

## MPFR - The GNU MPFR Library

- Project: The GNU MPFR Library
- Website: https://www.mpfr.org/
- License: GNU LGPL

MPFR is used indirectly through `gmp-wasm` for arbitrary-precision floating-point operations.

本作品では、MPFRも `gmp-wasm` 経由で利用しています。  
GMP/MPFRの開発者の皆様に感謝します。

---

## WebGPU

- Specification / API: WebGPU
- Related documentation: https://developer.mozilla.org/docs/Web/API/WebGPU_API

Mandel Zoom Abyss uses WebGPU for real-time GPU rendering.

The shader runs the Mandelbrot perturbation calculation in parallel over the screen pixels.  
Storage buffers are used to pass the CPU-generated reference orbit and palette LUT to the GPU.

本作品では、WebGPUのstorage bufferを使って、CPU側で生成した基準軌道と色LUTをGPUへ渡しています。  
WebGL2では難しかった構成を、WebGPUによってかなり素直に実装できるようになりました。

---

## TOMOQ1024 / Mandelbrot-Set-Viewer

- Project: Mandelbrot-Set-Viewer
- Repository: https://github.com/TOMOQ1024/Mandelbrot-Set-Viewer
- License: MIT License
- Author: TOMOQ1024

The color design of Mandel Zoom Abyss was inspired by TOMOQ1024's Mandelbrot-Set-Viewer.

配色設計については、TOMOQ1024氏の Mandelbrot-Set-Viewer の設計を参考にさせて頂きました。  
氏の配色がとても好きなんです。  
素晴らしい作品をありがとうございます。

Mandel Zoom Abyss does not copy source code from Mandelbrot-Set-Viewer.  
The implementation and palette ramps in this project are independent, but the color design influence is acknowledged here.

---

## Mandelbrot perturbation rendering references

Mandel Zoom Abyss uses the general idea of perturbation rendering:

- A high-precision reference orbit is computed on the CPU.
- Nearby pixels are evaluated as lower-precision deltas from that reference orbit on the GPU.

This technique is known in deep-zoom Mandelbrot rendering culture and related public fractal rendering research.  
This project is an original WebGPU/WebAssembly implementation guided by that general idea.

本作品では、CPU側のGMP多倍長計算と、GPU側のf32摂動計算を組み合わせています。  
すべてのピクセルを多倍長で直接計算するのではなく、基準軌道だけを高精度にし、周辺ピクセルをGPUで高速に処理することで、ブラウザ上でリアルタイム性を維持しています。

---

## AI-assisted implementation

Some implementation work was assisted by AI tools.

技術実装にはAI支援も利用しています。  
ただし、システム設計、描画思想、最適化方針、WebGPU + WebAssembly GMP + 摂動法の組み合わせ、演出設計は作者によるものです。

---

## Project license

Mandel Zoom Abyss source code is released under the MIT License.

Copyright (c) 2026 ぼいち

The source code is licensed MIT.

Rendered images and videos created using this source code are licensed under:

CC BY-NC-SA 4.0  
https://creativecommons.org/licenses/by-nc-sa/4.0/

Where a citation is listed, please also check the license of the citing source.
