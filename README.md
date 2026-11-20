# Mountain tunnel collapse simulator (tunnel_sim) and window app — companion source for the book

Design documents and code for the mountain tunnel collapse simulator built in ***Toward a Million Lines XIX — Building a Mountain-Tunnel Collapse Simulator*** (Japanese title 『LLM で 100 万行のソフトウェア開発 XIX — 山岳トンネルの崩壊のシミュレータをつくる』; the book is published in Japanese and English).

`tunnel_sim` (Python) computes how a water-saturated mountain collapses when a tunnel is excavated in it. The mountain and a weak band are sets of **bonded particles** (the discrete element method); the water inside is solved as **steady seepage**, and buoyancy and seepage force are applied to each particle. It excavates in three ways: a **cross-section whose semicircular radius grows** stage by stage, a **longitudinal section** in which the face advances into a weak band, and a **three-dimensional half mountain** with the same advance. It handles a weakened surface layer, a deep mountain with a water-stop wall, and surcharge, and writes 2-D and 3-D animations and figures. The computation core is one; it runs on the **CPU or on a GPU** (numba-cuda), and large computations are run unattended as a **batch** on a GPU desktop machine. A Windows **window app** (Flutter) sets the parameters, starts the computation, shows progress and plays the animations. **The window holds no computation of its own**: every button runs a `tunnel_sim` command and reads the result files it writes. In this project **the design documents are the source of the code**.

The case study of the book is the collapse of the tunnel-face crown and the cave-in of the ground surface in the Kamikura section of the Iiyama Tunnel (2003). It is an example: the simulator is not specific to it, it is **not a reproduction or a forecast**, and it is **not for judging the safety of any real tunnel**. What the verification (50 tasks, all passed on a real GPU machine) confirms is only that the code solves the equations of the design documents as designed; the book states what cannot be said.

## Download

**The ready-to-run app and the source are not in this repository's files; they are on the [Releases](../../releases) page.** The release has four separate ZIPs:

| File | Contents |
|:---|:---|
| `tunnel_exe.zip` | The Windows window app, ready built (**Japanese screens**), with the simulator it runs (Japanese display) and a small-example launcher |
| `tunnel_exe_en.zip` | The same app with **English screens** and the **English-display simulator** (`src`) |
| `tunnel.zip` | Design documents (`docs/`, Japanese, L1-L4, the source; `docs_en/`, the complete set for English readers: L1-L3 translated into English, L4 the Japanese originals as is) in separate folders, the code (`src/`, Japanese display; `src_en/`, the same simulator with English display strings; `app/`), the requirements specification, empty databases (`ledger/`), and the tools that build the batch package for the GPU machine |
| `tunnel_animations.zip` | The animations of three calculations of the book's verification (a 2-D cross-section example, a 2-D advancing deep mountain, a 3-D deep mountain), MP4 only (H.264) |

The app needs Python 3.13 and numpy, scipy, numba, matplotlib and pillow on your PC (`requirements.txt` inside the ZIPs); a GPU needs numba-cuda and an NVIDIA driver (CUDA 12.8 or newer for sm_120). Extract to a short path. There is **no APK** (the app is a Windows desktop app). The app is **not code-signed**, so Windows may warn you. Calculation results and tests are not included, and the batch package for the GPU machine (`tunnel_batch.zip`, about 170 MB with Python and its parts) is not included either: it is built with the tools in `tunnel.zip`. No external data is needed. The first run takes a few minutes (numba compiles); try the bundled small example first (about 2 minutes on a CPU). Use a laptop only for checks; run large 3-D calculations on a GPU machine.

You are free to change the design documents and the code and compare the results.

---

## License

- **The author holds the copyright.**
- **The code is under the GNU General Public License v3.0 or later (GPL-3.0-or-later).** The full text is [`LICENSE`](LICENSE). **If you modify it and distribute it, you must publish the source under the same GPL-3.0-or-later terms.**
- **The design documents and the text are under the Creative Commons Attribution-ShareAlike 4.0 International license (CC BY-SA 4.0).** This covers `docs/`, `docs_en/`, the READMEs and the other written text of this repository, and the text of the matching book. See [`LICENSE-DOCS.md`](LICENSE-DOCS.md).
- **If you use them, say so.** State where it came from (the title of the book and the name of this repository) and keep the copyright notice. If you changed it, say that you changed it.
- **In this project the design documents are the source of the code.** When you publish something made from this code, **publish the design documents together with the code.**
- Third-party components (numpy, scipy, numba, matplotlib, pillow, numba-cuda; the Flutter engine inside the EXEs) remain under their own original licenses.
- Provided "as is", without warranty — as the GPL-3.0 text says.

## 著作権とライセンス

- **著作権は、著者にあります。**
- **コードは、GNU General Public License v3.0 以降（GPL-3.0-or-later）です。**全文は [`LICENSE`](LICENSE) です。**改変して配布するときは、同じ GPL-3.0 以降の条件で、ソースを公開する義務があります。**
- **設計書と文章は、Creative Commons 表示-継承 4.0 国際（CC BY-SA 4.0）です。**このリポジトリの `docs/`・`docs_en/`・README ほかの文章と、対応する本の文章が当たります。内容は [`LICENSE-DOCS.md`](LICENSE-DOCS.md) です。
- **使ったときは、使ったことを書いてください。**どこから使ったか（本の題名と、このリポジトリの名前）と、著作権の表示を、使った先に書いてください。直したときは、直したことも書いてください。
- **このプロジェクトでは、設計書がコードの源です。**コードを使って作ったものを公開するときは、**設計書も、コードと一緒に公開してください。**
- 第三者の部品（numpy・scipy・numba・matplotlib・pillow・numba-cuda、EXE の中の Flutter の engine）は、それぞれの元のライセンスのままです。
- 現状のまま（as is）提供します。保証はありません（GPL-3.0 の全文のとおりです）。
