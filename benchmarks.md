## Benchmarks

### Introduction

Baseline results obtained using the `tfcaidm` pipeline. These results can act as a leaderboard for individuals interested in benchmarking their different models and methodologies. A user can submit their results by running an automated script which will be provided in the near future. The script will take as input a trained model and output a performance score.

### Datasets

| Dataset      | Description | Annotation   | Additional Information | # Training Samples | # Validation Samples |
| ------------ | ----------- | ------------ | ---------------------- | ------------------ | -------------------- |
| xr_pna       | xray        | segmentation |                        |                    |                      |         
| ct_pna       | ct          | segmentation |                        |                    |                      |         
| kits         | ct          | segmentation |                        |                    |                      |         
| brats        | mri         | segmentation |                        |                    |                      |         

---

### Results

| Dataset | Task             | Model  | Training Scheme                            | Metrics | Score ↑|
| ------- | ---------------- | ------ | ------------------------------------------ | ------- | -----  |
| xr_pna  | segmentation     | unet   | pixel-wise classification w/ class weights | F1      |        |
| xr_pna  | segmentation     | unet++ | pixel-wise classification w/ class weights | F1      |        |
| xr_pna  | segmentation     | unet3+ | pixel-wise classification w/ class weights | F1      |        |

---

| Dataset | Task             | Model  | Training Scheme                            | Metrics | Score ↑|
| ------- | ---------------- | ------ | ------------------------------------------ | ------- | -----  |
| ct_pna  | segmentation     | unet   | pixel-wise classification w/ class weights | F1      |        |
| ct_pna  | segmentation     | unet++ | pixel-wise classification w/ class weights | F1      |        |
| ct_pna  | segmentation     | unet3+ | pixel-wise classification w/ class weights | F1      |        |