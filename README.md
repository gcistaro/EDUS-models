# EDUS models

Ab-initio tight-binding models and interaction files used by the regression tests of
[EDUS](https://github.com/gcistaro/EDUS). In the EDUS repository this is the git submodule
`tb_models/ab_initio`:

```bash
git submodule update --init tb_models/ab_initio
```

## Content

| Material | Bands (filled) | Hamiltonian | Gap (eV) | Interaction |
|----------|----------------|-------------|----------|-------------|
| Si       | 8 (4)          | `Si/Si_8bands_DFT_tb.dat` (DFT)   | 0.55 (indirect) | `Si/Si_8bands_{bare,screen}coulomb_qG0.txt` |
| Si       | 8 (4)          | `Si/Si_8bands_KCW_tb.dat` (KCW)   | 1.40 (indirect) | same as above |
| GaAs     | 8 (4)          | `GaAs/GaAs_8bands_KCW_tb.dat` (KCW) | 1.56 (direct) | `GaAs/GaAs_8bands_{bare,screen}coulomb_qG0.txt` |
| LiF      | 10 (5)         | `LiF/LiF_10bands_KCW_tb.dat` (KCW)  | 15.3 (direct) | `LiF/LiF_10bands_{bare,screen}coulomb_qG0.txt` |

The gaps are computed from the `tb.dat` files on a 12x12x12 k grid.

- `*_tb.dat`: Wannier Hamiltonian and position operator in the wannier90 `seedname_tb.dat` format.
  In the EDUS input: `"tb_file": ".../Si_8bands_KCW"` (without `_tb.dat`).
- `*coulomb_qG0.txt`: bare and screened interaction between Wannier functions, computed with KCW
  on the 8x8x8 cell (R in [-4,3]^3, 512 R vectors). In the EDUS input: `"bare_file"` and
  `"screen_file"`, with `"method": "hsex"` and `"read_interaction": true`.
  Use a grid that contains all the R vectors of the file (e.g. 9x9x9 or larger).

## Origin

Copied from [gcistaro/inputs_KCW-EDUS](https://github.com/gcistaro/inputs_KCW-EDUS)
(commit `75f77ee6faef`):

| File | Source |
|------|--------|
| `Si/Si_8bands_KCW_tb.dat`   | `MCarchive/MODELS/Si/8bands_s-3p/wan_tb.dat` |
| `Si/Si_8bands_DFT_tb.dat`   | `MCarchive/MODELS/Si/8bands_s-3p_DFT/wan_tb.dat` |
| `Si/Si_8bands_*coulomb_qG0.txt` | `MCarchive/MODELS/Si/8bands_s-3p/*coulomb_qG0.txt` |
| `GaAs/GaAs_8bands_KCW_tb.dat` | `Figures_asof_202606/MODELS/GaAs/wan_tb.dat` |
| `GaAs/GaAs_8bands_*coulomb_qG0.txt` | `Figures_asof_202606/MODELS/GaAs/*coulomb_qG0.txt` |
| `LiF/LiF_10bands_KCW_tb.dat` | `Figures_asof_202606/MODELS/LiF/10bands/wan_tb.dat` |
| `LiF/LiF_10bands_*coulomb_qG0.txt` | `Figures_asof_202606/MODELS/LiF/10bands/*coulomb_qG0.txt` |

The KCW models come from the `02-Wme` step of the KCW workflow (Wannier functions and
interaction on top of the KCW Hamiltonian); the DFT model of Si from the Wannierization of the
DFT bands with the same projections (`8bands_s-3p`).

The files must not be modified: the references of the EDUS tests depend on them.
To change a model, add a new file and update the tests.
