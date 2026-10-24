# gmid_SKY130

**gm/ID characterization data and plotting scripts for the SkyWater SKY130 open-source PDK.**

This repository contains ngspice sweep data for the SKY130 NMOS and PMOS devices, the Xschem testbenches that produced it, and Python scripts that turn it into the standard gm/ID design charts. Use it to size transistors with the gm/ID methodology.

### 🔗 Interactive gm/ID tool website

Explore this data in your browser, no install needed. Copy the URL below and open it:

```
https://nithinpuru.github.io/gmid/sky130a/
```

All PDKs (SKY130A, GF180MCU-D, IHP SG13G2):

```
https://nithinpuru.github.io/gmid/
```

---

## Contents

| Path | What's inside |
|---|---|
| [`gmid Data/`](gmid%20Data) | Raw sweep results, one folder per device and one `.txt` file per channel length |
| [`gmid Python Scipts/`](gmid%20Python%20Scipts) | One plotting script per device (interactive Matplotlib with per-length toggles) |
| [`GMID_Plot.ipynb`](GMID_Plot.ipynb) | Jupyter notebook that lets you pick any device from a menu |
| [`Design-Files/`](Design-Files) | Xschem testbenches (`.sch`) used to generate the data |

## Characterized devices

All devices use **W = 2 µm**, with Vgs swept in 0.1 mV steps (0.05 V to 1.8 V for the 1.8 V devices, up to 5 V for the 5 V devices).

| Device folder | SKY130 model | Lengths (µm) | Script |
|---|---|---|---|
| `nfet3_01v8_lvt` | `sky130_fd_pr__nfet_01v8_lvt` | 0.15, 0.25, 0.5 – 3 | `NMOS-LVT.py` |
| `nfet3_01v8_svt` | `sky130_fd_pr__nfet_01v8` | 0.15, 0.25, 0.5 – 3 | `NMOS-SVT.py`, `NMOS-SVT-negative.py` |
| `nfet_g5v0d10v5` | `sky130_fd_pr__nfet_g5v0d10v5` | 0.5 – 3 | `NMOS_g5v0d10v5.py` |
| `pfet3_01v8_lvt` | `sky130_fd_pr__pfet_01v8_lvt` | 0.35, 0.4, 0.5 – 3 | `PMOS-LVT.py` |
| `pfet3_01v8_svt` | `sky130_fd_pr__pfet_01v8` | 0.35, 0.4, 0.5 – 3 | `PMOS-SVT.py`, `PMOS-SVT-negative.py` |
| `pfet3_01v8_hvt` | `sky130_fd_pr__pfet_01v8_hvt` | 0.35, 0.4, 0.5 – 3 | `PMOS-HVT.py` |
| `pfet_g5v0d10v5` | `sky130_fd_pr__pfet_g5v0d10v5` | 0.5 – 3 | `PMOS_g5v0d10v5.py` |

"0.5 – 3" means 0.5 µm to 3 µm in 0.25 µm steps.

`NMOS-SVT.py` only plots points with Vov > 0 (strong inversion). The `-negative` variants also include Vov < 0, so you can see weak inversion.

## Plots generated

Each script draws one curve per channel length for:

- **gm/ID vs Vgs** and **gm/ID vs Vov**
- **gm/gds vs gm/ID**: intrinsic gain
- **ID/W vs gm/ID**: current density, for sizing W
- **fT vs gm/ID**: transit frequency, fT = gm / (2π·Cgg)
- **Cgd/Cgg** and **Cgs/Cgg vs gm/ID**

Use the checkboxes next to each plot to show or hide individual lengths. The axes rescale automatically.

## Getting started

```bash
git clone https://github.com/chennakeshavadasa/gmid_SKY130.git
cd gmid_SKY130
pip install numpy matplotlib
```

Run any device script. The scripts find the data in `gmid Data/` on their own, so you don't need to edit any paths:

```bash
python "gmid Python Scipts/NMOS-LVT.py"
```

Each plot opens in its own window. Close it to see the next one.

To use the notebook, start Jupyter from the repository root and run the cell:

```bash
pip install notebook
jupyter notebook GMID_Plot.ipynb
```

If you keep the data somewhere else, change `path` at the top of a script, or `base_dir` in the notebook.

## Data format

Each `.txt` file is an ngspice `wrdata` dump with 14 whitespace-separated columns. The sweep variable (Vgs) is repeated before every quantity:

| Column | 1 | 2 | 4 | 6 | 8 | 10 | 12 | 14 |
|---|---|---|---|---|---|---|---|---|
| Quantity | Vgs | gm | Id | Vth | gds | Cgg | Cgs | Cgd |

The number in each filename (`gmid_nmos_<N>_...`) is the length index N, in the order listed in the table above.

## Regenerating the data

The testbenches in `Design-Files/` are made for [Xschem](https://xschem.sourceforge.io/) and [ngspice](https://ngspice.sourceforge.io/) with the SKY130 PDK installed, for example with the [IIC-OSIC-TOOLS](https://github.com/iic-jku/IIC-OSIC-TOOLS) container. Before you simulate, update the `wrdata` output paths in the `.sch` files, which currently point to `/foss/designs/PDKCHAR/`.

## Related

- [gm/ID Explorer](https://nithinpuru.github.io/gmid/): interactive web tool for SKY130A, GF180MCU-D and IHP SG13G2
- [gmid_SKY130A](https://github.com/chennakeshavadasa/gmid_SKY130A): source of the SKY130A web explorer
- [SkyWater SKY130 PDK documentation](https://skywater-pdk.readthedocs.io)

## Acknowledgements

Special thanks to [**Soumya Kanta Rana**](https://www.linkedin.com/in/soumya-rana/) for the testbench.

## License

See [LICENSE](LICENSE).
