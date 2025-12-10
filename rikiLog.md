1. Simply follow README instructions.

2. Changed CUDA version to 13.0 in Dockerfile.

```
pip install -U torch torchvision torchaudio
```
was needed for compatibility so added to Dockerfile.

3. After building the docker image, run the container with the following command:
```
docker run -i -v "$(pwd):/tdmpc2" --gpus all -t riki/tdmpc2:1.0.1 /bin/bash
```
Added wandb_project and wandb_entity values to config.yaml.

4. For evaluating checkpoints, needed to install dependencies for Meta-World.
Followed environment.yaml
Degraded wheel, setuptools and gym.

5. Errors:
The error AttributeError: 'TensorDict' object has no attribute '_tensordict' is caused by a version mismatch between your newly installed PyTorch (v2.8.0) and the tensordict library.
Fix (bypass):
Add compile=false to command


6. For mani-skill2:
Changed Dockerfile to use Python 3.9.
```
pip install mani-skill2==0.4.1
python -m mani_skill2.utils.download_asset all (once)
export MS2_ASSET_DIR=/tdmpc2/tdmpc2/data
```

Running Tests:
```
python train.py task=cheetah-run-backwards compile=false
```

Successful Tests:
```
python train.py task=dog-run steps=70
python train.py task=walker-walk compile=false
```

Unsuccessful Tests:
Running mt80 (installing gym is a pain...)
```
python train.py task=pick-ycb (This also requires gym as well...)
```
