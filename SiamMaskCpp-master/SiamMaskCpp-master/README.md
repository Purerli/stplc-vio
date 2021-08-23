# SiamMaskCpp
* C++ Implementation of [SiamMask](https://github.com/foolwood/SiamMask)
* Porting slogan:
    * numpy operations &rarr; cv::Mat operations
    * CNNs &rarr; torch::jit::script::Module
    * Other tensor operations &rarr; torch::Tensor operations
* Faster than the original implementation (speed increased from 22fps to 40fps when tested with a single NVIDIA GeForce GTX 1070)

# Requirements
* OpenCV >= 3 (tested with 3.4.0)
* PyTorch >= 1 (tested with 1.3.0)

# Convert a SiamMask model to Torch scripts
You can use the models (with the refine module) trained with the original repository [foolwood/SiamMask](https://github.com/foolwood/SiamMask) for inference in C++. Just Follow the instruction in [jiwoong-choi/SiamMask](https://github.com/jiwoong-choi/SiamMask#converting-siammask-model-with-the-refine-module-to-torch-scripts) to convert your own models to Torch script files.

# Download pretrained Torch scripts
Or you can download pretrained Torch scripts. These files are converted from the pretrained models ([SiamMask_DAVIS.pth](http://www.robots.ox.ac.uk/~qwang/SiamMask_DAVIS.pth) and [SiamMask_VOT.pth](http://www.robots.ox.ac.uk/~qwang/SiamMask_VOT.pth)) in the original repository.

```bash
git clone --recurse-submodules https://github.com/nearthlab/SiamMaskCpp
cd SiamMaskCpp
mkdir models
cd models
wget https://github.com/nearthlab/SiamMaskCpp/releases/download/v1.0/SiamMask_DAVIS.tar.gz
wget https://github.com/nearthlab/SiamMaskCpp/releases/download/v1.0/SiamMask_VOT.tar.gz
tar -xvzf SiamMask_DAVIS.tar.gz
tar -xvzf SiamMask_VOT.tar.gz
```

Before building demo, make sure the following command prints out the correct path to torch install directory.
```bash
python3 -c "import torch; print(torch.__path__[0])"
# /path/to/lib/python3.x/site-packages/torch
```

# How to build demo
```bash
cd SiamMaskCpp
mkdir build
cd build
# specify -DTORCH_PATH=/path/to/lib/python3.x/site-packages/torch if cmake fails to detect PyTorch automatically
cmake ..
make

# Move the executable file to the repository directory
mv demo ..
```

# How to run demo
```bash
cd SiamMaskCpp
./demo -c config_davis.json -m models/SiamMask_DAVIS tennis
./demo -c config_vot.json -m models/SiamMask_VOT tennis
```
