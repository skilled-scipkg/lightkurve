# Evidence: lightkurve-build-and-install

## Primary docs
- `docs/source/development/index.rst`
- `docs/README.rst`
- `docs/source/development/contributing.rst`
- `docs/source/about/install.rst`
- `docs/source/development/documentation.rst`
- `docs/source/about/citing.rst`

## Primary source entry points
- `skills/lightkurve-build-and-install/references/doc_map.md`
- `src/lightkurve/__init__.py`
- `src/lightkurve/seismology/__init__.py`
- `src/lightkurve/prf/__init__.py`
- `src/lightkurve/io/__init__.py`
- `src/lightkurve/correctors/__init__.py`
- `src/lightkurve/config/__init__.py`
- `src/lightkurve/seismology/core.py`
- `src/lightkurve/prf/tpfmodel.py`
- `src/lightkurve/prf/prfmodel.py`
- `src/lightkurve/version.py`
- `src/lightkurve/utils.py`
- `src/lightkurve/units.py`
- `src/lightkurve/time.py`
- `src/lightkurve/targetpixelfile.py`
- `src/lightkurve/search.py`
- `src/lightkurve/periodogram.py`
- `src/lightkurve/lightcurvefile.py`
- `src/lightkurve/lightcurve.py`
- `src/lightkurve/interact_bls.py`

## Extracted headings
- (none extracted)

## Executable command hints
- $ git clone https://github.com/YOUR-GITHUB-USERNAME/lightkurve.git
- $ cd lightkurve
- $ curl -sSL https://install.python-poetry.org | python -
- $ poetry install
- $ poetry run python YOUR-SCRIPT.py
- $ poetry run jupyter notebook
- $ poetry run pytest  # runs all the unit tests
- Python environment as follows:
- $ python -m pip install .
- $ python -m pip uninstall lightkurve
- $ python -m pip install --editable .  # creates the symbolic link
- $ git remote add upstream https://github.com/lightkurve/lightkurve.git

## Warnings and pitfalls
- If you encounter the error ``Pandoc wasn't found``, you will have to install ``pandoc`` separately as well following its `installation instruction <https://pandoc.org/installing.html>`_  .
