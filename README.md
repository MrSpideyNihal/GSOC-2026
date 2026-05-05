# GSoC 2026 — MetaCall
## Code Coverage and Memory Tracking Improvements for MetaCall Core

**Organization:** [MetaCall](https://metacall.io)  
**Official Repo:** [metacall/core](https://github.com/metacall/core)  
**Contributor:** [MrSpideyNihal](https://github.com/MrSpideyNihal)  
**Mentor:** Vicente Eduardo Ferrer Garcia ([@viferga](https://github.com/viferga))

---

## Project Description

This project improves code coverage reporting and memory tracking reliability across platforms in MetaCall Core. The work focuses on extending Valgrind and MemorySanitizer (MSan) support, reducing false positives in sanitizer runs, adding reproducible instrumentation tooling, and improving CI observability.

---

## Merged PRs ✅

| # | Title | Date |
|---|-------|------|
| [#706](https://github.com/metacall/core/pull/706) | ci: add memcheck argument to metacall-environment and metacall-configure scripts | Mar 24 |
| [#723](https://github.com/metacall/core/pull/723) | fix(memcheck): add ruby suppression and remove duplicate wasm suppression | Mar 25 |
| [#726](https://github.com/metacall/core/pull/726) | fix(detour): free handle struct in detour_unload() to prevent memory leak | Mar 26 |
| [#736](https://github.com/metacall/core/pull/736) | feat(msan): add clang install and memory sanitizer configuration | Mar 28 |
| [#743](https://github.com/metacall/core/pull/743) | ci: add linux memory sanitizer test job | Mar 30 |
| [#763](https://github.com/metacall/core/pull/763) | chore: add tools/instrumentation folder with MSan and Valgrind helpers | Apr 2026 |

---

## Task Progress

### Memory Tracking & Valgrind

| Task | Status |
|------|--------|
| Set up Valgrind memcheck pipeline in CI | ✅ Done |
| Add memcheck flags to environment and configure scripts | ✅ Done |
| Ruby suppression — reduce false positives | ✅ Done |
| Reduce Valgrind errors: 62,205 → 104 | ✅ Done |
| Python + Valgrind standalone Docker image | ✅ Done |

### MemorySanitizer (MSan)

| Task | Status |
|------|--------|
| Install clang and configure MSan build | ✅ Done |
| Add MSan CI job to linux-test.yml | ✅ Done |
| Add compile-time ignorelist for gtest false positives | ✅ Done |
| Add runtime MSAN_OPTIONS suppressions | ✅ Done |
| Reduce CodeLocation false positives: 294 → ~3 | ✅ Done |
| Fix ext_loader real memory leak | 🔄 In Progress |
| Add dedicated MSan CI yml file | ⏳ Pending |

### Memory Leaks

| Task | Status |
|------|--------|
| Fix detour handle struct memory leak | ✅ Done |
| Fix py_loader missing Py_XDECREF (PR #764) | 🔄 Open PR |
| Investigate ext_loader uninitialized value | 🔄 In Progress |

### Instrumentation Tooling

| Task | Status |
|------|--------|
| MSan standalone Dockerfile (PoC) | ✅ Done |
| Valgrind/Python standalone Dockerfile | ✅ Done |
| Restructure tools/instrumentation folder | ✅ Done |
| Wire ignorelist into cmake pipeline | ✅ Done |

### CI / Observability

| Task | Status |
|------|--------|
| Add memcheck to CI pipeline | ✅ Done |
| Add MSan job to CI | ✅ Done |
| Add dedicated MSan yml file | ⏳ Pending |
| ARM64 / PPC64 debugging | ⏳ Pending |

---

## GSoC Project

**Title:** Code Coverage and Memory Tracking Improvements  
**Size:** Small (90 hours) | **Difficulty:** High  
**Mentors:** Vicente Eduardo Ferrer Garcia, Thomas Rory Gummerson, Fernando Vaño Garcia
