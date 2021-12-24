## Benchmarks

### Introduction

Baseline results obtained using the `tfcaidm` pipeline. These results can act as a leaderboard for individuals interested in benchmarking their different models and methodologies. A user can submit their results by writing a few lines of code, with examples shown below. For those new to the lab, this is a great place to start!

Note: Benchmarks are currently only supported on the CAIDM clusters, additionally, [tfcaidm](https://github.com/Brandhsu/tfcaidm) must be installed.

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

<table>
  <thead>
    <tr>
      <th>Dataset</th>
      <th>Client</th>
      <th>Description</th>
      <th>Annotation</th>
      <th>Inputs</th>
      <th>Outputs</th>
      <th>Additional Information</th>
      <th># Evaluation Samples</th>
      <th>Fold</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ct/kits</td>
      <td>/data/ymls/client-2d.yml</td>
      <td>2D kidney tumor segmentation</td>
      <td>tumor segmentation</td>
      <td><code>["dat"]</code></td>
      <td><code>["lbl"]</code></td>
      <td>
        <a
          href="https://colab.research.google.com/github/peterchang77/caidm/blob/master/datasets/ct-kidney-kits/segmentation.ipynb"
          >ct-kidney-kits</a
        >
      </td>
      <td></td>
      <td>0</td>
    </tr>
    <tr>
      <td>ct/pna</td>
      <td>/data/ymls/client.yml</td>
      <td>2D pneumonia segmentation</td>
      <td>pneumonia segmentation</td>
      <td><code>["dat", "lng"]</code></td>
      <td><code>["pna"]</code></td>
      <td>
        <a
          href="https://colab.research.google.com/github/peterchang77/caidm/blob/master/datasets/ct-lung-pna/segmentation.ipynb"
          >ct-lung-pna</a
        >
      </td>
      <td></td>
      <td>0</td>
    </tr>
    <tr>
      <td>mr/brats</td>
      <td>/data/ymls/client-5-class.yml</td>
      <td>2D brain tumor segmentation</td>
      <td>tumor segmentation</td>
      <td><code>["t2", "flair", "pre", "post"]</code></td>
      <td><code>["lbl"]</code></td>
      <td>
        <a
          href="https://colab.research.google.com/github/peterchang77/caidm/blob/master/datasets/mr-brain-tumor/segmentation.ipynb"
          >mr-brain-tumor</a
        >
      </td>
      <td></td>
      <td>0</td>
    </tr>
    <tr>
      <td>mr/breast-fgt</td>
      <td>/data/ymls/client-3-class.yml</td>
      <td>2D breast fibroglandular tissue segmentation</td>
      <td>fibroglandular tissue segmentation</td>
      <td><code>["dat"]</code></td>
      <td><code>["lbl"]</code></td>
      <td>
        <a
          href="https://colab.research.google.com/github/peterchang77/caidm/blob/master/datasets/mr-breast-fgt/segmentation.ipynb"
          >mr-breast-fgt</a
        >
      </td>
      <td></td>
      <td>0</td>
    </tr>
  </tbody>
</table>

---

### Results

<table>
  <thead>
    <tr>
      <th>Rank</th>
      <th>User</th>
      <th>Dataset</th>
      <th>Model</th>
      <th># Params</th>
      <th>Description</th>
      <th>Metrics</th>
      <th>Score ↑</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>tfcaidm</td>
      <td>ct/pna</td>
      <td>unet</td>
      <td></td>
      <td>pixel classifier w/ class weights</td>
      <td>F1</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>2</td>
      <td>tfcaidm</td>
      <td>ct/pna</td>
      <td>unet++</td>
      <td></td>
      <td>pixel classifier w/ class weights</td>
      <td>F1</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>3</td>
      <td>tfcaidm</td>
      <td>ct/pna</td>
      <td>unet3+</td>
      <td></td>
      <td>pixel classifier w/ class weights</td>
      <td>F1</td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
