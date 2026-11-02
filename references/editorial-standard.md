# Editorial & solution audit standard — logn.ac

## Mandatory editorial blueprint

1. **题意与约束**：忠实解释问题，列出影响复杂度的关键约束及部分分。
2. **暴力做法**：建模、完整 C++14 可提交代码、时间/空间复杂度、适用的数据规模或子任务、失效原因。
3. **从暴力到正解**：指出重复计算、冗余枚举或结构性质，推导为何可优化。
4. **正解**：核心思想、严格但易读的正确性证明、时间/空间复杂度、完整 C++14 可提交代码。
5. **其他本质不同的解法（如存在）**：通常合计展示 2–3 种值得教学的解法。若问题适合，可展示“暴力 + 两种独立正解”；如仅有一种合理正解，不必凑数。每种解法有各自完整代码和验证结果。
6. **比较与易错点**：说明各解法适用数据范围、区别、关键边界、常见 WA/TLE。

Do not label an algorithm full-score if it only covers subtasks. Do not assume an official solution is flawless, and do not treat agreement between two implementations sharing the same mistake as proof.

## Source style

- C++14; `#include <bits/stdc++.h>` and `using namespace std;`; normal `int main()`.
- Prefer procedural functions and ordinary globals/local arrays, `vector<int> g[N]` for ordinary graph adjacency lists.
- Avoid unnecessary classes, generic libraries, elaborate design patterns, C++17 syntax, or chain-forward-star representation for normal graph exercises.
- Explicitly choose `int`/`long long` based on provable numeric upper bounds; respect memory and recursion limits.
- Each fenced C++ listing is **complete and independently buildable**, not a fragment. Keep actual code text synchronized byte-for-byte (or a generated extract with hash) with tested sources.
- Do not silently switch the algorithm when rewriting code for publication; recompile and retest after **any** edits.

## Independent verification workflow

- Re-derive constraints and an algorithmic proof without presuming a website explanation is correct.
- Author an independent small-domain oracle (`brute.cpp`). Exhaust tiny state spaces when feasible.
- Author `reference.cpp` and all alternatives. Compile with `g++ -std=c++14 -O2 -Wall -Wextra` and test sanitizer builds when appropriate.
- Write `stress/generator.py` and `stress/stress.py`. Use fixed seeds; validate generated inputs before execution; compare using the actual problem checker semantics; log run totals, seed, command and mismatches; save and minimize failures.
- Test samples, exhaustive small cases, random medium cases, carefully constructed counterexamples and maximal performance/memory. Test multi-case aggregate constraints.
- For each editorial solution, test only within its declared correctness/performance domain, and report exactly what was executed.
- Use deliberately buggy baselines, if available, to assess test-suite discriminatory power; they do not substitute for independent oracle checks.
- If any relevant check fails or the independent oracle is infeasible without alternative validation, mark it and escalate to review rather than asserting certainty.

## `editorial-audit.md` minimum fields

| Field | What to record |
|---|---|
| Source consistency | Statement/constraints and subtask fidelity |
| Approach list | Algorithm name, brute/partial/full designation |
| Code audit | File path, SHA256, compilation result |
| Proof | Core invariant or proof and unresolved concerns |
| Samples | Passed/total for **each** approach |
| Differential tests | Compared/total, seed ranges, applicable domain |
| Max tests | Input sizes, runtime, memory, target limitations |
| Editorial publication | Not published / approved / published; never auto-expose during contest |
| Final gate | `EDITORIAL_VERIFIED` or `BLOCKED_EDITORIAL` |

## Example project tree

```text
problem-id/
├── source.json
├── statement.md
├── statement-audit.md
├── constraints.yaml
├── tags.json
├── editorial.md
├── editorial-audit.md
├── solutions/
│   ├── README.md
│   ├── brute.cpp
│   ├── reference.cpp
│   └── alternative-1.cpp            # only if substantive
├── stress/
│   ├── README.md
│   ├── generator.py
│   ├── stress.py
│   └── failures/                   # stored reproduction cases
├── tests/
│   └── manifest.json
├── verification.json
├── validation-report.md
└── hydro-import/                    # target-version-dependent
```

## Detailed presentation and render gate (required)

Read `visual-math-standard.md`. Organize every solution as **problem interpretation → hand-worked example → naive enumeration and code → bottleneck → optimized insight → staged algorithm with a trace diagram → invariant/lemma/proof → complete commented code → derived complexity → traps and comparison**. Use intermediate states, not just the final state. When multiple algorithms differ materially, repeat the trace and proof for each, and clearly compare trade-offs.

Each published C++ source uses a fenced `cpp` block and must be the identical tested file. Highlighting comes from Hydro's renderer; confirm that the actual syntax-highlighting feature is enabled and visible. Add focused Chinese comments explaining tricky operations, not every line. Include a small variable/state dictionary outside code when useful.

Math must use target-renderer-compatible LaTeX with explicit initial states, induction ranges, index domains and justified transformations. Record rendered equations, linked figures and code highlighting in `editorial-render-audit.md` and do not claim editorial publication readiness until visual checks pass.
