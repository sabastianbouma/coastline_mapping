# Coastline mapping

An exploratory project for extracting a coastline from satellite imagery, following the [ArcGIS Python coastline-extraction tutorial](https://developers.arcgis.com/python/latest/samples/coastline-extraction-usa-landsat8-multispectral-imagery/).

## Get started

If `conda` is not recognized, install Miniforge (a Conda distribution) first.
On an Apple silicon Mac with Homebrew, run:

```bash
brew install --cask miniforge
```

Initialize Conda for Bash, then close and reopen Terminal:

```bash
conda init bash
```

If you use a different shell, replace `bash` with `zsh` or the shell you use.
Verify that `conda --version` works before continuing.

Create the project environment from the repository root:

```bash
conda env create --file environment.yml
conda activate coastline
```

The environment installs the project in editable mode, so Python can import it
from `src/coastline` while you work. In VS Code, open the notebook and select
the `coastline` Python environment as its kernel. Then open
[`notebooks/01_coastline_extraction.ipynb`](notebooks/01_coastline_extraction.ipynb)
and work through its sections.

If you change the dependencies in `environment.yml`, update the existing
environment with:

```bash
conda env update --file environment.yml --prune
```

The notebook uses `GIS("home")` as a starting point for signing in. Configure
ArcGIS authentication in your local ArcGIS environment before running
ArcGIS-dependent cells; do not put passwords or access tokens in the notebook.
Some image services and analysis operations may require an ArcGIS account with
the appropriate access.

## Project layout

```text
.
├── data/
│   ├── raw/             # Source data; keep large/local files out of Git
│   └── processed/       # Intermediate data; keep generated files out of Git
├── notebooks/           # Step-by-step exploration and visual analysis
├── outputs/             # Generated maps, figures, and exported results
├── src/
│   └── coastline/       # Reusable Python code, imported as `coastline`
├── environment.yml      # Conda environment used for analysis
└── pyproject.toml        # Python package metadata and build configuration
```

### What the Python configuration files do

- **`environment.yml`** tells Conda which Python version and packages to
  install. It also installs this repository in editable mode (`-e .`), so
  changes to package code are available without reinstalling.
- **`pyproject.toml`** describes the Python package: its name, version,
  supported Python version, runtime dependencies, and how setuptools finds
  packages under `src/`. It is not a replacement for the Conda environment;
  Conda is used here because the ArcGIS Python API is installed from Esri's
  Conda channel.
- **`src/coastline/__init__.py`** marks `coastline` as an importable Python
  package and defines its version. Python runs this file when you import
  `coastline`; you normally do not run it directly. The double-underscore
  spelling (`__init__.py`) is significant.
- **`notebooks/01_coastline_extraction.ipynb`** is the interactive workflow.
  Keep analysis steps and maps here; move reusable functions into
  `src/coastline/` as the project grows.

The `raw`, `processed`, and `outputs` folders are intended for local or
generated files. Their contents are ignored by Git, except for `.gitkeep`
placeholders, so large rasters and outputs are not accidentally committed.