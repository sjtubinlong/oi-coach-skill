# Illustrated explanation and mathematical presentation standard — logn.ac

## Goal and editorial structure

Produce a student-readable, rigorous NOIP/CSP lesson, not a short answer. Be as detailed as necessary for a reader familiar with the prerequisite concepts to reproduce the approach, but omit repetitive filler. Every new problem has a brute solver and a fully verified reference solver; meaningfully distinct approaches (often 2–3 total) are documented when justified.

Recommended order:

1. Problem interpretation: objective, legal operations, input/output, actual constraints, and a small example separate from official samples.
2. Brute force: exact enumeration/search, complete trace for the small example, full commented C++14 code, complexity and which subtasks it covers.
3. Transition: identify repeated work and the mathematical/property-based reason an optimization is possible; add a before/after diagram when useful.
4. Full solution: define symbols/data structures or DP states; build the algorithm in numbered steps, each with its changing state; cover initialization, transitions, termination and answer extraction.
5. Proof: assumptions, key lemma/invariant, base case, induction/exchange/contradiction steps, conclusion. Separate intuition from proof.
6. Complexity: derive operation counts and memory usage, including sorting, data structure operations, and aggregate-test constraints.
7. Full independently verified C++14 code and a table comparing approaches; common WA/TLE and counterexamples.

## Illustrations are evidence, not decoration

- Choose a diagram matched to the algorithm: indexed array with highlighted active ranges, dual-pointer timeline, segment tree node ranges, queue content over BFS layers, DFS stack/tree, graph relaxation snapshots, sorted greedy picks, DP state matrix with arrows, sweep line events, binary search bounds, union-find components, etc.
- For a procedure with more than one consequential state change, show **initial → key transitions → final** (either several figures, one labeled multipart figure or an accurate trace table plus figure). Identify each step with the same labels and indices as the text and code.
- Every image needs a descriptive caption and alt text; diagrams must remain readable at reasonable phone and desktop widths, with adequate contrast and no cropped labels. Assets are stored under `editorial-assets/` with relative links and source edit files if applicable. Verify file existence and, where possible, check diagram values against a programmatic trace.
- Prefer SVG for crisp static schematic diagrams, PNG for raster figures, and Markdown tables/number lines for comparisons. Mermaid may be used *only* after testing Hydro's actual renderer; otherwise export as SVG/PNG and link the image. Do not assume client JS or arbitrary HTML is allowed. No remote links necessary for local diagram assets.
- Do not insert forced diagrams for purely symbolic transformations; an aligned derivation or well-formatted table can convey steps better.
- **Do not alter statement figures**; editorial figures are new, separately tracked teaching assets. Do not copy images without permission.

## LaTeX and mathematical derivation

- Use `$...$` and `$$...$$` when tested on target Hydro, with verified alternate syntax only if the platform requires it.
- Define all variables and domains; show intermediate algebraic steps and justify each equality/inequality. Define recurrence boundaries, e.g. `$dp[0]=0$`, unreachable states, index ranges, and modulo treatment.
- For DP: state meaning → transition enumeration → recurrence → initial conditions → valid evaluation order → answer. For greedy: exchange proof or staying-ahead invariant. For graphs: graph model, invariant, operation trace and edge cases. For number theory: assumptions, lemmas and transformations.
- Use `\begin{aligned} ... \end{aligned}` in display math only if compatible with the renderer. Avoid giant one-line equations and manually verify escaped backslashes, braces, subscripts, superscripts, inequality symbols, floors/ceilings, and line wrapping.
- Derive time and space bounds from loops/data structures; do not claim `$O(n\log n)$` merely because a standard template is used.

## Syntax highlighted, annotated NOIP-style code

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;
    vector<ll> a(n + 1);
    for (int i = 1; i <= n; i++) cin >> a[i];

    // 示例：前缀和 pre[i] 表示前 i 个数之和。
    // 用 long long 防止较大的元素和发生 int 溢出。
    vector<ll> pre(n + 1, 0);
    for (int i = 1; i <= n; i++) {
        pre[i] = pre[i - 1] + a[i];
    }

    cout << pre[n] << '\n';
    return 0;
}
```

This example illustrates **comment density and formatting only**; it is not a substitute for problem-specific verified code. Every actual editorial block must be separately compiled and tested byte-for-byte (or source-linked to a tested hash). Explain nontrivial branches, invariants, and risk points; avoid meaningless annotations such as `i++ // increment i`.

## Render verification and acceptance

Create `editorial-render-audit.md` with:

- Renderer target: Hydro version, theme, Markdown plugin/highlighter, math renderer if known; preview URL/screenshot identifier and inspection date.
- Code blocks: number, each `cpp` language marker, visible syntax highlighting, overflow/scroll behaviour, exact source hashes, no clipped code.
- Math: count of inline/display formulas, rendered pass/fail and missing glyphs/escaped delimiters; responsive check for long equations.
- Figures: asset list, physical file, insertion location, caption/alt text, source/editability, checked trace state and visual legibility.
- Layout: tables, narrow screen, light/dark themes if applicable; captions and image sizing.
- Result: `RENDER_VERIFIED` or `RENDER_NOT_VERIFIED`, with actionable defects. A screenshot-free text inspection alone cannot assert visual verification.

An editorial may be called `EDITORIAL_VERIFIED` only when its solution code passes its documented tests and the rendered page passes this audit. Otherwise report `BLOCKED_EDITORIAL` for publication. Keep problem-only import gate separate.
