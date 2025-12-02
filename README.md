# 2.4 GHz Microstrip Patch Antenna (Keysight ADS)

## Project Overview
- Single-layer microstrip patch antenna designed for the 2.4 GHz ISM band.
- Implemented and simulated in Keysight ADS 2020 using Momentum EM solver.
- Meets the design brief of using an FR4 substrate, maintaining a footprint below 50 mm × 50 mm, and targeting gain ≥ 2.5 dBi with radiation efficiency ≥ 50 %.

## Layout and Stackup Highlights
- Stackup (`MyLibrary_lib/substrate1.subst`): FR-4 core (εr ≈ 4.4) with 1.6 mm thickness, 35 µm copper cladding on both sides.
- Layout extents derived from `simulation/MyLibrary_lib/231240/layout/emSetup_MoM/proj.gdf`: 45.40 mm (x-axis) × 39.40 mm (y-axis), satisfying the ≤ 50 mm × 50 mm requirement.
- Single 50 Ω microstrip feed (`P1`) defined in `simulation/.../proj.prt` and `proj_out.prt`.
- EM setup saved as `emSetup_MoM` under `simulation/MyLibrary_lib/231240/layout/`.

## Simulation Workflow
1. Launch ADS and open the workspace file `MyWorkspace_wrk/231240.dds`.
2. In the Project Tree, expand `MyLibrary_lib > 231240 > layout` and open the layout view to inspect geometry.
3. Confirm the substrate assignment (`Substrate1`) via **EM > Substrate > Select**.
4. To rerun the EM simulation:
   - Right-click `emSetup_MoM` and choose **Simulate**.
   - Momentum uses the configuration stored in `proj.opt`, sweeping an adaptive frequency range from 83 MHz to 3 GHz with denser sampling around resonance.
5. Results are stored in the dataset `_231240_MomUW.ds` inside the `data/` directory; ADS automatically links this dataset to data displays.

## Inspecting Results
- **Return Loss (S11):** Create a Data Display (`.dds`) or open an existing one to plot `dB(S(1,1))`. Verify that |S11| ≤ −10 dB near 2.4 GHz.
- **Radiation Metrics:** Use **EM > Results > Radiation Pattern** on `emSetup_MoM` to generate 3D/2D plots. Ensure peak gain ≥ 2.5 dBi and radiation efficiency ≥ 50 % at 2.4 GHz. When generated, the radiation data is saved alongside the workspace in `data/EMAntenna.ds`.
- Document measured bandwidth, gain, and efficiency values in this README once extracted from the ADS data display.

## Repository Layout
- `231240.dds` – Workspace definition for Keysight ADS.
- `MyLibrary_lib/231240/` – Library cells for schematic and layout views of the antenna.
- `MyLibrary_lib/substrate1.subst` – Substrate definition (material stackup and layer assignments).
- `simulation/MyLibrary_lib/231240/layout/emSetup_MoM/` – Momentum EM setup files, mesh, and solver configuration.
- `data/` – ADS datasets containing S-parameters and radiation pattern results from the latest simulation run.

## Validation Checklist
- [ ] Re-run Momentum simulation and confirm convergence without errors.
- [ ] Plot S11 and record resonant frequency, bandwidth, and matching level.
- [ ] Generate far-field radiation report to log peak gain, efficiency, and beamwidth.
- [ ] Update this README with the validated numerical results and any tuning notes.

## Next Steps
- Fine-tune the feed or slot dimensions if the measured gain or efficiency falls short of targets.
- Export Gerber/ODB++ files from the layout if fabrication is planned; ensure manufacturing constraints are reflected in the design rules.
- Compare simulation data with lab measurements once a prototype is fabricated and note any discrepancies for model refinement.
