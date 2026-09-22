# Tests

`harness.cpp` holds logic tests for the mod, compiled together with it and with
the Windhawk API stubbed out. They cover:

- the color table and its generations;
- the content scope, and the node draws that open one;
- the palette highlight and its luminance matching;
- the UXP rewrite, all of it: the stylesheet, including that a border
  past the ceiling is recolored while text at the same value is not, and the
  design tokens in the panel's own script, including that an icon stroke and a
  loose string beside them are left alone by that pass; and the stylesheet
  text a script or a webview page carries — injected rules, a theme's table of
  backgrounds — taken while an icon's own hex stays as it is, a call such as
  `setRgb(18, 18, 18)` is not a color, and a token is converted once;
- the file redirect on real temporary files, for a stylesheet and for a script,
  including that the copy carries the extension of the file it stands in for,
  and that only files under After Effects' own `Support Files\UXP\plugins`
  folder are taken;
- the custom theme fields, checked against the defaults the settings block
  itself ships, including a whole theme written as #RRGGBBAA by a color picker
  — the alpha is dropped rather than the field refused — and the theme the mod
  writes out for sharing, which is written for every palette and never carries
  an alpha back;
- every built-in palette against the rules the readme states: a rising ramp,
  text and accent that carry, and a highlight white can sit on;
- that the palette list in the settings block, the palette tables in the mod's
  readme, and the palettes in the code are all the same set;
- the module ranges, including a dva module that unloads;
- which windows the frame work is spent on: top level, and with a frame;
- the menu theme bookkeeping;
- how the renamed dvaui functions are counted, and how a renamed dvaui is
  found by its exports;
- the popup swatches under either of their names, the six arguments 26.3 gives
  them passed through in order, inside a content scope.

Run them from the repository root, with Windhawk and PowerShell 7 installed:

    pwsh tests/run.ps1

The script first builds the mod itself with Windhawk's compiler and
`-Wall -Wextra`, then builds and runs the tests at `-O2` and at `-O0`. It exits
non-zero if anything fails to build or any test fails.
