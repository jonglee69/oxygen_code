# Particle size vs. Oxygen Relationship calculator

Calculates the oxygen content of Ti, Zr and Hf powders covered by a surface oxide (MO₂) layer, as a function of particle diameter and oxide thickness.

**▶ Run it in your browser: https://jonglee69.github.io/oxygen_code/**

## Web calculator (`index.html`)
- Input: metal (Ti / Zr / Hf), metal and oxide densities, particle diameter (µm), oxide thickness (nm)
- Output: oxygen content (wt.%), specific surface area (m²/g), oxide volume fraction
- Inverse calculation: oxide thickness that gives a target oxygen content, and the minimum particle size that keeps oxygen below a target
- Log–log plot for a list of oxide thicknesses and CSV download

No installation is needed; everything runs in the browser.

## Model
A spherical particle of diameter *D* carries a uniform oxide shell of thickness *t* (r = D/2):

- V_core = 4π(r − t)³/3, V_shell = 4πr³/3 − V_core
- O (wt.%) = 100 · ρ_ox·V_shell·f_O / (ρ_M·V_core + ρ_ox·V_shell), with f_O = 2M_O / (M_M + 2M_O)
- SSA (m²/g) = 6 / (ρ_M · D[µm])

Default densities (g/cm³): Ti 4.506, TiO₂ 4.23 (rutile), Zr 6.52, ZrO₂ 5.68, Hf 13.31, HfO₂ 9.68.

**Correction (Nov 2026):** versions of `particle_ssa_oxygen.ipynb` before commit `ed2dcda` used ρ_M·V_particle (whole sphere) instead of ρ_M·V_core for the metal mass. This counted the shell volume twice and underestimated oxygen by about 6t/D — e.g. 2.10 vs 2.22 wt.% at 1 µm with a 10 nm oxide, 18.1 vs 34.8 wt.% at 0.2 µm with 50 nm, and less than 1 % for particles above 10 µm. Select **"Original notebook formula"** in the web calculator (or use the `*_legacy` CSV columns) to reproduce the earlier curves.

## Notebook
`particle_ssa_oxygen.ipynb` — Python script (NumPy, Matplotlib). `oxygen_wt(D_um, t_nm, metal="Ti")` returns the oxygen content; the notebook writes a CSV (corrected and legacy columns) and plots Ti with 5, 10, 20 and 50 nm oxide layers.

## License
MIT © 2025 JongHyeon Lee, Nanomaterial Processing Lab, Chungnam National University
