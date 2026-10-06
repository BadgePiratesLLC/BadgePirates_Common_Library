# BadgePirates_Common_Library

Common KiCAD Library, FootPrint, and logos

## Status

Maintained

## Known footprint exceptions

- `BadgePiratesFootprint.pretty/Proto_TFT.kicad_mod` — 14-pin TH header, generic
  pad names only (1-14), no manufacturer part number, no silkscreen ID, no 3D
  model block. Source part is unidentified (checked twice, 2026-10-04/06; no
  git history shows a prior assignment). Not currently referenced by any board
  in this workspace (`grep -rl Proto_TFT` across /Users/kevinb/Code returns
  nothing) — not fab-blocking. Exempted from the 3D-model/part-ID gate as a
  placeholder footprint until someone identifies the physical part it was
  pulled from (board, datasheet, or part in hand). Nexus 7514f363.
