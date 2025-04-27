## Dataset Overview
This dataset contains histopathology images of colon cells collected from 99 different patients.
It is prepared specifically for the COSC2793 Computational Machine Learning Assignment 2 project: Colon Cancer Cell Classification.

Each image is labeled for one or both of the following tasks:

Task 1 (Binary Classification):
Determine if a given cell image represents a cancerous (isCancerous = 1) or non-cancerous (isCancerous = 0) cell.

Task 2 (Multi-Class Classification):
Classify the cell into one of the following types:
* fibroblast
* inflammatory
* epithelial
* other

## Files
* data_labels_mainData.csv:
  * Label file for the first 60 patients.
  * Includes both isCancerous and cell_type columns.
* data_labels_extraData.csv:
  * Label file for the additional 39 patients.
  * Includes only isCancerous column (no cell_type annotation).
* patch_images/:
  * Contains all 27x27 pixel RGB images representing individual colon cells.
