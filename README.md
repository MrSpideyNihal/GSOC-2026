# GSoC 2026 Final Work Submission

**Contributor:** Nihal Rodge ([@MrSpideyNihal](https://github.com/MrSpideyNihal))

**Organization:** MetaCall

**Project:** Code Coverage and Memory Tracking Improvements

**Mentor:** [@viferga](https://github.com/viferga),Mostafa Wael 

**Project size:** Small (90 hours)

**Synopsis:** [metacall/gsoc-2026 — Code Coverage and Memory Tracking Improvements](https://github.com/metacall/gsoc-2026#3-code-coverage-and-memory-tracking-improvements)
**Contact:** nihalrodge01@gmail.com · [LinkedIn](https://linkedin.com/in/nihalrodge)

---

## 1. Project Goals

The MetaCall runtime's memory tracking mechanism was very basic and could not detect leaks in detail, and several tests were failing silently on architectures like ARM64/PPC64 in CI without meaningful error messages. This project set out to:

- Extend and harden support for existing memory-diagnostic tools (Valgrind, AddressSanitizer) for automated testing.
- Investigate and implement Memory Sanitizer (MSan) integration as a deeper, more precise diagnostic layer.
- Improve observability in CI — clearer logs, traces, and actionable error messages for hard-to-reproduce bugs.
- Fix real memory bugs uncovered by this tooling along the way.

## 2. What I Did

Over the course of GSoC I built out a full MSan CI/CD pipeline for MetaCall from the ground up, alongside parallel hardening of the existing Valgrind/memcheck pipeline. Key pieces of work, roughly in chronological order:

- **Valgrind/memcheck baseline (Mar):** Added a `memcheck` argument to the `metacall-environment` and `metacall-configure` scripts and a dedicated `valgrind-memcheck` CI job, then fixed suppression files (Ruby, WASM duplicate) to remove noise from the existing Valgrind pipeline.
- **Real memory bug fix (Mar 25):** Fixed a memory leak in `detour_unload()` where the handle struct was never freed — found via the improved memory tooling.
- **MSan bring-up (Mar 26–30):** Added Clang install + Memory Sanitizer configuration, wired `CC`/`CXX` env vars correctly for the Clang compiler path, added an independent `clang` configure option, and added dedicated `linux-clang-test` and `linux-memory-sanitizer` CI jobs.
- **Instrumentation tooling layout (Apr):** Restructured the project into a `tools/instrumentation` folder holding both MSan and python-valgrind helper scripts, added gtest MSan instrumentation build support, and wrote Dockerfile + usage docs for both instrumentation paths.
- **MSan ignorelist system (May 1–5):** Built out the MSan ignorelist and suppression-wiring mechanism so known false positives (e.g. in third-party deps) don't block CI, with correct CMake tab-indentation formatting for `CompileOptions.cmake`.
- **Real memory bug fix (May 16):** Fixed an uninitialized `set_iterator` in `adt_trie.c`, discovered through the two-stage MSan bootstrap process, alongside implementing that two-stage bootstrap itself (Stage 1: build Clang + `compiler-rt`; Stage 2: build an MSan-instrumented `libc++` against it) — necessary because MSan requires all linked code, including the C++ standard library, to be instrumented to avoid false positives.
- **FreeBSD support (May 21):** Added a wildcard symlink for `clang-*` binaries post-install to support MSan builds on FreeBSD.
- **Valgrind refresh (May 6):** Updated Python suppressions to Python 3.13 and added a `max-stackframe` flag to handle larger stack frames without false Valgrind errors.
- **Ignorelist correctness (Jun 12):** Fixed the googlebenchmark ignorelist path to correctly match its actual `_deps/googlebenchmark-src` build location.
- **Documentation (Jun 16):** Wrote a full "Docker MSan local development workflow" doc (section 8.1.3) so future contributors can reproduce the MSan environment locally instead of only in CI.
- **CI matrix expansion (Jul 18):** Added a combined Clang AddressSanitizer + ThreadSanitizer CI matrix, extending the sanitizer coverage beyond MSan alone, plus fixes for a rustup-nightly guard and Cargo executable path debugging in the CMake configure step.

## 3. Current State

- The MSan two-stage bootstrap pipeline is merged and running in CI (`develop` branch).
- ASan and ThreadSanitizer CI matrix is merged and running alongside MSan.
- The Valgrind/memcheck pipeline has updated, accurate suppressions for Python 3.13, Ruby, and WASM.
- A documented, reproducible local Docker workflow exists for developers to run MSan builds outside CI.
- Two real memory bugs (a `detour_unload()` leak and an uninitialized `adt_trie` iterator) found via this tooling have been fixed upstream.
- All PRs listed below are merged into `metacall:develop`.

## 4. What's Left

Two items are in progress and expected to be finished shortly after this submission:

| Item | Status |
|---|---|
| Helgrind (thread-error detector) integration | Changes done, testing remaining |
| Ruby instrumentation for the sanitizer/instrumentation pipeline | Changes done, testing remaining |

## 5. Merged Pull Requests

All PRs below were merged by mentor [@viferga](https://github.com/viferga) into `metacall:develop`.

| # | Title | Merged | Diff |
|---|---|---|---|
| [#847](https://github.com/metacall/core/pull/847) | ci(clang): add Clang AddressSanitizer and ThreadSanitizer CI matrix | Jul 18, 2026 | +23 / -2 |
| [#823](https://github.com/metacall/core/pull/823) | docs: add Docker MSan local development workflow (section 8.1.3) | Jun 18, 2026 | +88 / -0 |
| [#818](https://github.com/metacall/core/pull/818) | fix(msan): correct googlebenchmark ignorelist path to match `_deps/googlebenchmark-src` | Jun 12, 2026 | +1 / -1 |
| [#797](https://github.com/metacall/core/pull/797) | fix(msan): two-stage bootstrap and fix uninitialized `set_iterator` in `adt_trie` | May 22, 2026 | +59 / -42 |
| [#791](https://github.com/metacall/core/pull/791) | fix(valgrind): add max-stackframe flag and update python suppressions to 3.13 | May 6, 2026 | +199 / -52 |
| [#787](https://github.com/metacall/core/pull/787) | chore: add MSan ignorelist and instrumentation helpers | May 5, 2026 | -83 |
| [#763](https://github.com/metacall/core/pull/763) | chore: add tools/instrumentation folder with MSan and python-valgrind scripts | Apr 25, 2026 | +276 / -2 |
| [#743](https://github.com/metacall/core/pull/743) | ci: add linux memory sanitizer test job | Mar 30, 2026 | +59 / -13 |
| [#736](https://github.com/metacall/core/pull/736) | feat(msan): add clang install and memory sanitizer configuration | Mar 28, 2026 | +93 / -3 |
| [#726](https://github.com/metacall/core/pull/726) | fix(detour): free handle struct in `detour_unload()` to prevent memory leak | Mar 26, 2026 | +2 / -0 |
| [#723](https://github.com/metacall/core/pull/723) | fix(memcheck): add ruby suppression and remove duplicate wasm suppression | Mar 25, 2026 | +27 / -1 |
| [#706](https://github.com/metacall/core/pull/706) | ci: add memcheck argument to metacall-environment and metacall-configure scripts | Mar 24, 2026 | +56 / -1 |

Full list is also viewable live at: [github.com/metacall/core/pulls?q=is:pr+is:merged+author:MrSpideyNihal](https://github.com/metacall/core/pulls?q=is:pr+is:merged+author:MrSpideyNihal)

## 6. Challenges & Lessons Learned

- **MSan requires a fully instrumented stack.** A single-stage MSan build produces constant false positives because uninstrumented C++ standard library code looks "uninitialized" to the sanitizer. The two-stage bootstrap (build Clang + `compiler-rt` first, then build an MSan-instrumented `libc++` against it) was the key insight that made the whole pipeline usable, and is now documented for future contributors.
- **Ignorelists need to track real build paths, not assumed ones.** The googlebenchmark ignorelist fix (#818) was a reminder that third-party dependency paths can shift (e.g. `_deps/googlebenchmark-src`), and ignorelists silently stop working if not kept in sync.
- **Cross-platform sanitizer support is fragile.** Getting MSan working on FreeBSD required a `clang-*` wildcard symlink fix that wasn't needed on Linux — a good example of how sanitizer tooling assumptions baked in for one platform don't transfer directly.
- **Working with a direct, Socratic mentor.** My mentor, viferga, teaches through probing questions rather than direct answers, which pushed me to verify claims before proposing fixes rather than guessing. Two habits this instilled: always run the fork's own CI before pushing anything upstream, and never suggest a fix without a verifiable source (a stack trace, a sanitizer log, or documentation) backing it.
- **CI observability matters as much as the fix itself.** Several PRs here (e.g. #743, #847) weren't just "add sanitizer" but "add sanitizer *and* make its failures debuggable" — without clear CI job separation and logging, an intermittent ARM64/PPC64-style failure is nearly impossible to track down.

---
