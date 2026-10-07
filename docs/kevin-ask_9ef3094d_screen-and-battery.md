# Nexus 9ef3094d — Kevin action needed (d0144 corrections)

**UPDATE 2026-10-07:** Item 1 (battery holder STEP) below is RESOLVED — do
not action it. The real Keystone-53 STEP was pulled via
`easyeda2kicad --lcsc_id=C5352788` (no DigiKey login needed after all),
landed in the library at commit `66e0904`, and re-pointed into both CC15 and
BlueTeamTool's BT1/BT2 footprint instances (cc15 `1cd67a7`, BTT `c018901`).
3d-model-check passes on both boards. The original ask text is kept below
only for history.

Only **item 2 (screen module calipers)** is still outstanding and still
needs Kevin/Jared's hands on the physical part.

## 1. Battery holder — Keystone 53 real STEP — ~~RESOLVED, see update above~~

Research so far (DigiKey + Keystone parametric data, via search — keyelco.com
and digikey.com both return HTTP 403 to automated fetch from this box, so the
exact manufacturer drawing could not be pulled directly):

- Keystone **53** (DigiKey PN 2745544) is listed by DigiKey's own parametric
  table as **"Number of Cells: 1"** — i.e. ONE unit of part 53 is a complete
  single-cell SMT clip (positive spring end + negative flat-tab end on one
  stamped part), not a half-clip that needs a second part for the other
  terminal.
- **PCB Pad Pitch: 52.10mm (AA) | 28.40mm (CR2)** — this is the spacing
  between the part's own two solder pads, sized to the cell it holds. CC15
  uses a 14500 cell, which is AA-length (50mm) — so the **AA pitch, 52.10mm,
  is the correct spacing**, one Keystone 53 per cell.
- Height above board: 0.569in (14.45mm), matches Kevin's d0144 note.
- ~~Not yet confirmed: exact clip width/depth/shape and true mated height~~ —
  superseded, the real STEP (easyeda2kicad, C5352788) has the actual geometry.

~~Ask: download the real Keystone STEP...~~ — not needed, resolved via
easyeda2kicad instead. See update at top of file.

## 2. Screen module — physical calipers measurement

Confirmed part: AliExpress 3.2" "B" variant, item 3256805739551171 — ILI9341
320x240 with capacitive FT6336U touch, no SD slot (P2 removed per Kevin's
seller request). The `simple-circuit.com` page Kevin linked is FORM-FACTOR
reference only (that page's module is a different, resistive-touch + SD
variant) — do not copy its dimensions.

No public datasheet exists for this specific harvested listing's mechanical
dims. **Ask: with calipers on the physical module Kevin has, measure and
report:**

1. Header pin count, pitch (should be 2.54mm, confirm), and position relative
   to the PCB edge/corners
2. Full module PCB outline (length x width, corner radii if any)
3. Mounting hole positions (all 4 corners, hole diameter)
4. Glass/LCD active-area offset from the PCB edge (so the fab/courtyard
   outline on J3 lines up with the visible glass, not just the carrier PCB)
5. The actual header + socket mated stack height Kevin intends to use (so the
   3D model stands the module off the main board by the real amount, not a
   guessed value) — state which connector/socket pair this is

Once these are in hand: rotate the `Display-IL19341V-BP version` footprint
180° (module sits ABOVE the main board on its header, standing off — not
flush), rebuild the B.Fab/B.CrtYd outline and mounting holes from the real
numbers, and model the real stand-off height.

---
Filed by Bucky, Nexus 9ef3094d, 2026-10-06.
