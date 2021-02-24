# excel-examples

Use python to manipulate Excel files

## Environment

Use `conda` to build the python environment: `conda env create -f env.yml`

This will create a virtual environment named `excel-examples` with the following libraries:

- `jupyterlab` provides an interactive notebook interface
- `pandas` facilitates data I/O and other calculations
- `seaborn` allows you to create static visualizations
- `plotly` allows you to create interactive visualizations
- `xlsxwriter` is needed if you want to write data back into an excel file

After installing, activate the environment with: `conda activate excel-examples`

With the environment active, kick off the notebook server with `jupyter lab`
