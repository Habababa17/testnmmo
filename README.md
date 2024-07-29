![figure](https://neuralmmo.github.io/_static/banner.jpg)

# ![icon](https://neuralmmo.github.io/_build/html/_images/icon.png) Welcome to the Platform!

[Documentation](https://neuralmmo.github.io "Neural MMO Documentation") is hosted by github.io.
[![PyPI version](https://badge.fury.io/py/nmmo.svg)](https://badge.fury.io/py/nmmo)
[![](https://dcbadge.vercel.app/api/server/BkMmFUC?style=plastic)](https://discord.gg/BkMmFUC)
[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/cloudposse.svg?style=social&label=Follow%20%40jsuarez5341)](https://twitter.com/jsuarez5341)

## Installation

After cloning this repo, run:

```
pip install -e .[dev]
```

## Training

To test if the installation was successful (with the `--debug` mode), run the following command:

```
python train.py --debug --no-track
```

To log the training process, edit the wandb section in `config.yaml` and remove `--no-track` from the command line. The `config.yaml` file contains various configuration settings for the project.

### Agent zoo and your custom policy

This baseline comes with four different models under the `agent_zoo` directory: `neurips23_start_kit`, `yaofeng`, `takeru`, and `hybrid`. You can use any of these models by specifying the `-a` argument.

```
python train.py -a hybrid
```

You can also create your own policy by creating a new module under the `agent_zoo` directory, which should contain `Policy`, `Recurrent`, and `RewardWrapper` classes.

### Curriculum Learning using Syllabus

The training script supports automatic curriculum learning using the [Syllabus](https://github.com/RyanNavillus/Syllabus) library. To use it, add `--syllabus` to the command line.

```
python train.py --syllabus
```

## Replay generation

The `policies` directory contains a set of trained policies. For your models, create a directory and copy the checkpoint files to it. To generate a replay, run the following command:

```
python train.py -m replay -p policies
```

The replay file ends with `.replay.lzma`. You can view the replay using the [web viewer](https://kywch.github.io/nmmo-client/).

## Evaluation

The evaluation script supports the pvp and pve modes. The pve mode spawns all agents using only one policy. The pvp mode spawns groups of agents, each controlled by a different policy.

To evaluate models in the `policies` directory, run the following command:

```
python evaluate.py policies pvp -r 10
```

This generates 10 results json files in the same directory (by using `-r 10`), each of which contains the results from 200 episodes. Then the task completion metrics can be viewed using:

```
python analysis/proc_eval_result.py policies
```
