1. Simply follow README instructions.

Changed CUDA version to 13.0 in Dockerfile.

```
pip install -U torch torchvision torchaudio
```
was needed for compatibility so added to Dockerfile.

After building the docker image, run the container with the following command:
docker run -i -v "$(pwd):/tdmpc2" --gpus all -t riki/tdmpc2:1.0.1 /bin/bash

Added wandb_project and wandb_entity values to config.yaml.


For evaluating checkpoints, needed to install dependencies for Meta-World.
Followed environment.yaml
Degraded wheel, setuptools and gym.


Errors:
The error AttributeError: 'TensorDict' object has no attribute '_tensordict' is caused by a version mismatch between your newly installed PyTorch (v2.8.0) and the tensordict library.
Fix (bypass):
Add compile=false to command


Running Tests:
python train.py task=walker-walk compile=false

Successful Tests:
python train.py task=dog-run steps=70

Unsuccessful Tests:
Running mt80 (installing gym is a pain...)

