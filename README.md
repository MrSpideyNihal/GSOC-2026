# GSoC 2026 — MetaCall
## Code Coverage and Memory Tracking Improvements for MetaCall Core

**Organization:** [MetaCall](https://metacall.io)  
**Official Repo:** [metacall/core](https://github.com/metacall/core)  
**Contributor:** [MrSpideyNihal](https://github.com/MrSpideyNihal)  
**Mentor:** Raj Aryan, Mostafa Wael ,Vicente Eduardo Ferrer Garcia ([@viferga](https://github.com/viferga))


---

## Progress — 13/24 Tasks Done

| Task | Description | Status | PR |
|------|-------------|--------|----|
| Add memcheck to CI scripts | Add memcheck flags to environment and configure scripts | ✅ Done | [#706](https://github.com/metacall/core/pull/706) |
| Ruby Valgrind suppression | Add ruby suppression, remove duplicate wasm suppression | ✅ Done | [#723](https://github.com/metacall/core/pull/723) |
| Fix detour memory leak | Free handle struct in detour_unload() | ✅ Done | [#726](https://github.com/metacall/core/pull/726) |
| Configure MSan build | Install clang and configure memory sanitizer | ✅ Done | [#736](https://github.com/metacall/core/pull/736) |
| MSan CI job | Add linux memory sanitizer test job | ✅ Done | [#743](https://github.com/metacall/core/pull/743) |
| Instrumentation tooling | Add MSan and Valgrind instrumentation Dockerfiles | ✅ Done | [#763](https://github.com/metacall/core/pull/763) |
| Valgrind memcheck pipeline | Set up Valgrind memcheck in CI | ✅ Done | [#706](https://github.com/metacall/core/pull/706) |
| Reduce Valgrind errors | 62,205 → 104 errors with suppressions | ✅ Done | [#723](https://github.com/metacall/core/pull/723) |
| Python + Valgrind Docker | Standalone image for Python Valgrind testing | ✅ Done | [#763](https://github.com/metacall/core/pull/763) |
| MSan compile-time ignorelist | Suppress gtest false positives via -fsanitize-ignorelist | ✅ Done | [#763](https://github.com/metacall/core/pull/763) |
| MSan runtime suppressions | Wire MSAN_OPTIONS suppressions into build | ✅ Done | [#763](https://github.com/metacall/core/pull/763) |
| Reduce MSan false positives | CodeLocation errors: 294 → ~3 | ✅ Done | [#763](https://github.com/metacall/core/pull/763) |
| Fix py_loader memory leak | Add missing Py_XDECREF on inspect_signature results | 🔄 Open PR | [#764](https://github.com/metacall/core/pull/764) |
| Fix ext_loader uninitialized | Real MSan error in ext_loader_impl.cpp | 🔄 In Progress | — |
| Dedicated MSan CI yml | New workflow file for MSan testing | ⏳ Pending | — |
| Custom instrumentation layer | Lightweight allocation/deallocation tracking | ⏳ Pending | — |
| Code coverage reporting | Integrate coverage reporting into CI | ⏳ Pending | — |
| ARM64 / PPC64 debugging | Fix failing tests on ARM64 and PPC64 architectures | ⏳ Pending | — |
| Enhanced CI observability | Better logs and error messages in CI pipelines | ⏳ Pending | — |

---

## GSoC Project

**Title:** Code Coverage and Memory Tracking Improvements  
**Size:** Small (90 hours) | **Difficulty:** High  
**Mentors:** Vicente Eduardo Ferrer Garcia, Raj Aryan, Mostafa Wael 
