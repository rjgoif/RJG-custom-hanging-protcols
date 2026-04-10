# RJG Visage 7 Custom Hanging Protocols

Custom hanging protocols for CT and ultrasound, built on top of the MGH base protocols.

---

## ReeceMode (`ReeceMode.xml`)

**Base:** `ED CT.xml`

### Changes

**Prior depth extended to P7**
ED CT loads up to P4. ReeceMode adds P5–P7 — study definitions, image sets, and display set assignments — so up to 7 prior CT studies are available in layouts.

**Compare ED (2) redesigned**
The original `Compare ED (2)` layout used `_Layout_Neuro_ED_CT2` includes for both current and P1. Replaced with explicit AX/COR/SAG triplane columns using `_2D_WL`, with each plane linked by group so current and prior scroll together.

**CR Vessel MPR layout added**
New layout group for chest CT with a "CR Vessel Suppress" series. Uses custom server-side geometry tokens (`3T_sag1third` / `3T_vessel2thirds`) to give the vessel subtraction panel a wider panel than the standard MPR. Lung window defaults applied. Hidden automatically if no CR Vessel series is present.

**Compare 4 MPR: COR replaced with SAG**
The base `Compare 4 MPR` layout showed AX + COR per study. Changed to AX + SAG, and the `AnyListedMissing` condition on `CurrAllSeriesThinnest` was removed so the layout is always available.

**Prior-heavy axial MPR layouts added**
Four new layouts for scrolling through many time points at once, all using linked axial MPR:

| Layout | Geometry | Studies |
|---|---|---|
| 4 MPRax | `1x2\|1x2` | Curr + P1–P3 |
| 8 MPRax | `2x2\|2x2` | Curr + P1–P7 |
| 6 MPRax cols | `3x1\|3x1` | Curr + P1–P5 |
| 6 MPRax rows | `1x3\|1x3` | Curr + P1–P5 |

Panel ordering in these layouts is **row-first across monitors** (1 2 3 4 / 5 6 7 8, not 1 2 / 3 4 / 5 6 / 7 8), achieved by interleaving display set declarations rather than filling each monitor sequentially.

---

## R US (`R_US.xml`)

**Base:** `Ultrasound (no auto play).xml`

### Changes

**Compare Statics/Clips (80% statics) layouts added**
New layout group (LayoutIds 5201, 5210, 5212, 5213, 1–4 monitors) mirroring the existing `Compare Statics/Clips` layouts but with `Zoom="80%"` on all static image panels. Clip panels remain at default zoom. Useful when static frames are large-format and measurements are obscured by image numbers 100% (THYROIDS!)