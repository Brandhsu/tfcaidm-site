## Benchmarks

### Introduction

Baseline results obtained using the `tfcaidm` pipeline. These results can act as a leaderboard for individuals interested in benchmarking their different models and methodologies. A user can submit their results by running an automated script which will be provided in the near future. The script will take as input a trained model and output a performance score.

Note: [tfcaidm](https://github.com/Brandhsu/tfcaidm) must be installed to run a benchmark.

<details>

<summary>Getting started</summary>

To get started, users should checkout all related benchmark datasets and their descriptions using the `help` method. They can also checkout the current leaderboard standings with the `view_leaderboard` method. This site will be updated with the best submissions periodically, but for real-time updates, use the methods below.

```python
from tfcaidm import Benchmark

# --- Get benchmark related information
Benchmark.help()

# --- View the leaderboards
Benchmark.view_leaderboard()
```

</details>

<details>

To run a benchmark, a user needs to specify the benchmark dataset path and a trained model. From there they will have to align the dataset inputs and targets with their model inputs and outputs. After doing so, they will be able to run model evaluation and view their results. A submission can then optionally be made to the leaderboards.

<summary>Running a benchmark</summary>

```python
from tfcaidm import Model
from tfcaidm import Benchmark
from jarvis.utils.general import gpus

DATA_PATH = "benchmark/kits"
MODEL_PATH = "checkpoints/unet"

# --- Autoselect GPU (use only on caidm cluster)
gpus.autoselect()

# --- Load a trained model
model = Model.load_model(MODEL_PATH)

# --- Ensure model inputs and outputs matches the dataset inputs and targets
model = Model.inference_mode(model, inputs=["dat"], outputs=["lbl"])

# --- Instantiate a benchmark object
benchmark = Benchmark(DATA_PATH)

# --- Run model evaluation
benchmark.run(model)

# --- If you are happy with your score, submit it
benchmark.submit()
```

</details>

### Datasets

| Dataset | Description | Annotation   | Additional Information | # Training Samples | # Validation Samples |
| ------- | ----------- | ------------ | ---------------------- | ------------------ | -------------------- |
| xr_pna  | xray        | segmentation |                        |                    |                      |
| ct_pna  | ct          | segmentation |                        |                    |                      |
| kits    | ct          | segmentation |                        |                    |                      |
| brats   | mri         | segmentation |                        |                    |                      |

---

### Results

| User    | Dataset | Task         | Model  | # Parameters | Description                       | Metrics | Score ↑ | Date |
| ------- | ------- | ------------ | ------ | ------------ | --------------------------------- | ------- | ------- | ---- |
| tfcaidm | xr_pna  | segmentation | unet   |              | pixel classifier w/ class weights | F1      |         |      |
| tfcaidm | xr_pna  | segmentation | unet++ |              | pixel classifier w/ class weights | F1      |         |      |
| tfcaidm | xr_pna  | segmentation | unet3+ |              | pixel classifier w/ class weights | F1      |         |      |

---

| User    | Dataset | Task         | Model  | # Parameters | Description                       | Metrics | Score ↑ | Date |
| ------- | ------- | ------------ | ------ | ------------ | --------------------------------- | ------- | ------- | ---- |
| tfcaidm | ct_pna  | segmentation | unet   |              | pixel classifier w/ class weights | F1      |         |      |
| tfcaidm | ct_pna  | segmentation | unet++ |              | pixel classifier w/ class weights | F1      |         |      |
| tfcaidm | ct_pna  | segmentation | unet3+ |              | pixel classifier w/ class weights | F1      |         |      |
