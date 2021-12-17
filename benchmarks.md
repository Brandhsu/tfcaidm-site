## Benchmarks

### Introduction

Baseline results obtained using the `tfcaidm` pipeline. These results can act as a leaderboard for individuals interested in benchmarking their different models and methodologies. A user can submit their results by running an automated script which will be provided in the near future. The script will take as input a trained model and output a performance score.

Note: Benchmarks are currently only supported on the CAIDM clusters, additionally, [tfcaidm](https://github.com/Brandhsu/tfcaidm) must be installed to run a benchmark.

<details>

<summary>Getting started</summary>

To get started, users should checkout all related benchmark datasets and their descriptions using the `help` method. They can also checkout the current leaderboard standings with the `leaderboard` method. This site will be updated with the best submissions periodically, but for real-time updates, use the methods below.

```python
from tfcaidm import Benchmark

# --- Get benchmark related information
Benchmark.help()

# --- View the leaderboards
Benchmark.leaderboard()
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

| Dataset       | Client                        | Description                                  | Annotation                         | Inputs                           | Outputs   | Additional Information                                                                                                               | # Evaluation Samples | Fold |
| ------------- | ----------------------------- | -------------------------------------------- | ---------------------------------- | -------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------- | ---- |
| ct/kits       | /data/ymls/client-2d.yml      | 2D kidney tumor segmentation                 | tumor segmentation                 | `["dat"]`                        | `["lbl"]` | [ct-kidney-kits](https://colab.research.google.com/github/peterchang77/caidm/blob/master/datasets/ct-kidney-kits/segmentation.ipynb) |                      | 0    |
| ct/pna        | /data/ymls/client.yml         | 2D pneumonia segmentation                    | pneumonia segmentation             | `["dat", "lng"]`                 | `["pna"]` | [ct-lung-pna](https://colab.research.google.com/github/peterchang77/caidm/blob/master/datasets/ct-lung-pna/segmentation.ipynb)       |                      | 0    |
| mr/brats      | /data/ymls/client-5-class.yml | 2D brain tumor segmentation                  | tumor segmentation                 | `["t2", "flair", "pre", "post"]` | `["lbl"]` | [mr-brain-tumor](https://colab.research.google.com/github/peterchang77/caidm/blob/master/datasets/mr-brain-tumor/segmentation.ipynb) |                      | 0    |
| mr/breast-fgt | /data/ymls/client-3-class.yml | 2D breast fibroglandular tissue segmentation | fibroglandular tissue segmentation | `["dat"]`                        | `["lbl"]` | [mr-breast-fgt](https://colab.research.google.com/github/peterchang77/caidm/blob/master/datasets/mr-breast-fgt/segmentation.ipynb)   |                      | 0    |

---

### Results

| User    | Dataset | Task         | Model  | # Params | Description                       | Metrics | Score ↑ | Date |
| ------- | ------- | ------------ | ------ | -------- | --------------------------------- | ------- | ------- | ---- |
| tfcaidm | ct/pna  | segmentation | unet   |          | pixel classifier w/ class weights | F1      |         |      |
| tfcaidm | ct/pna  | segmentation | unet++ |          | pixel classifier w/ class weights | F1      |         |      |
| tfcaidm | ct/pna  | segmentation | unet3+ |          | pixel classifier w/ class weights | F1      |         |      |
