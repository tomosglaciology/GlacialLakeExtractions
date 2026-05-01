## Figure Scripts

This subfolder contains scripts and outputs for generating figures used in the project.

For each figure, you can expect the following files:

- **Jupyter Notebook (`.ipynb`)** – contains the code used to generate the figure  
- **Image file (`.png`)** – the final exported figure  
- **Data file (`.csv`)** – the dataset used to create the figure  

### Naming Convention

Files are grouped by figure and follow a consistent naming pattern:

- `FigureX.ipynb` – code used to generate the figure  
- `FigureX.png` – exported figure  
- `<descriptive_name>.csv` – data used in the figure  

### Example

- `Figure6.ipynb`  
- `Figure6.png`  
- `PixelMisclassificationResults.csv`  

### Notes

- Not all figures will have a `.csv` file if the data is derived from other sources or processed within the notebook.  
- An `environment.yml` file is provided to reproduce the computational environment required to run the notebooks.  
