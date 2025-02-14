# Pipeline for annotating cell types for sc-/sn-RNA-Seq Analysis in 10X Genomics data

## Usage

`run-cell-types-annotation.sh` is designed to be run as if it was called from this module directory even when called from outside of this directory.

Parameters according to the project and analysis strategy will need to be specified in the following scripts:
- `project_parameters.Config.yaml` located at the `root_dir`
- `future_globals_value` is hardwired coded in the `run-cell-types-annotation.R`. If necessary, user can increase/decrease resources.
- Celldex references are hardwired coded in the `run-cell-types-annotation.R`. User should modify the reference to be used according to their experiment.
- `run-cell-types-annotation.sh`: User should comment in/out the script to use based on the selection of the desired methods for cell type annotation.
- `04-merge-cell-types-annotations-all.R`: The user should run this script to merge cell type annotations from SingleR (both broad and fine resolutions). Additionally, if multiple annotation methods are used (current options include SingleR method and a gene marker list), this script will merge the annotations accordingly.


Please verify that the cell type names in your customized reference list match exactly with those in the `.figures/palettes/cell_types_palette.tsv`. If any cell types are missing, kindly submit an [issue](https://github.com/stjude-dnb-binfcore/sc-rna-seq-snap/issues) with the list of those cell types, and we will add them to the palette list.


### Run module on an interactive session on HPC within the container

To run all of the Rscripts in this module sequentially on an interactive session on HPC, please run the following command from an interactive compute node:

```
bash run-cell-types-annotation.sh
```

### Run module by using lsf on HPC within the container

There is also the option to run a lsf job on the HPC cluster by using the following command on an HPC node:

```
bsub < lsf-script.txt
```


## Folder content
This folder contains a script tasked to identify cell types annotation with SingleR by using a broad and fine resolution labeling across the project. There is also a script to identify and annotate cell types by using a list of gene markers.

## Folder structure 

The structure of this folder is as follows:

```
├── 01-cell-types-annotation-SingleR-broad.Rmd
├── 02-cell-types-annotation-SingleR-fine.Rmd
├── 03-cell-types-annotation-gene-markers.Rmd
├── 04-merge-cell-types-annotations-all.R
├── lsf_script.txt
├── plots
|   ├── 01_cell_types_annotation_SingleR_broad
|   |   ├── Report_cell_types_annotation_SingleR_broad_<Sys.Date()>.html
|   |   └── Report_cell_types_annotation_SingleR_broad_<Sys.Date()>.pdf
|   ├── 02_cell_types_annotation_SingleR_fine
|   |   ├── Report_cell_types_annotation_SingleR_fine_<Sys.Date()>.html
|   |   └──Report_cell_types_annotation_SingleR_fine_<Sys.Date()>.pdf
|   ├── 03_cell_types_annotation_gene_markers
|   |   ├── Report_cell_types_annotation_gene_markers_<Sys.Date()>.html
|   |   └── Report_cell_types_annotation_gene_markers_<Sys.Date()>.pdf
├── README.md
├── results
|   ├── 01_cell_types_annotation_SingleR_broad
|   ├── 02_cell_types_annotation_SingleR_fine
|   ├── 03_cell_types_annotation_gene_markers
|   └── 04_cell_types_annotations_all
├── run-cell-types-annotation-gene-markers.R
├── run-cell-types-annotation-SingleR.R
├── run-cell-types-annotation.sh
└── util
|___└── function-cell-type-fractions.R
```

