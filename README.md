# Install neural-style on OS X Mavericks
Directions from https://github.com/jcjohnson/neural-style

Did NOT install CUDA, cuDNN, or OpenCL backends <br>
(without GPU capabilities, need to run in CPU mode by setting flag -gpu -1)

## 1. Install torch and lua

In terminal:

```
$ git clone https://github.com/torch/distro.git ~/torch --recursive 
$ cd ~/torch; bash install-deps; # installs package dependencies 
$ ./install.sh # installs LuaJIT, Lua Rocks

$ cat .bash_profile >> .profile 
$ rm .bash_profile 
$ source ~/.profile # adds torch to PATH
```

To remove torch:

```
$ rm -rf ~/torch
```

Run torch from terminal:

```
$ th
```

Install with luarocks:

```
$ luarocks install torch 
$ luarocks install nn
$ luarocks install optim 
$ luarocks install lua-cjson
```

Install torch-hdf5 from GitHub: 

```
$ git clone https://github.com/deepmind/torch-hdf5
$ cd torch-hdf5 
$ luarocks make hdf5-0-0.rockspec
```

## 2. Install loadcaffe

```
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" # installs Homebrew
$ brew tap homebrew/versions
$ brew install protobuf
$ luarocks install loadcaffe 
```

## 3. Install neural-style

Clone neural-style: 

```
$ cd ~/
$ git clone https://github.com/jcjohnson/neural-style.git
$ cd neural-style
$ sh models/download_models.sh 
```

## 4. Test that everything installed correctly

```
$ th neural_style.lua -gpu -1 -print_iter 1
```

Should return:
```
Successfully loaded models/VGG_ILSVRC_19_layers.caffemodel
conv1_1: 64 3 3 3
conv1_2: 64 64 3 3
conv2_1: 128 64 3 3
conv2_2: 128 128 3 3
conv3_1: 256 128 3 3
conv3_2: 256 256 3 3
conv3_3: 256 256 3 3
conv3_4: 256 256 3 3
conv4_1: 512 256 3 3
conv4_2: 512 512 3 3
conv4_3: 512 512 3 3
conv4_4: 512 512 3 3
conv5_1: 512 512 3 3
conv5_2: 512 512 3 3
conv5_3: 512 512 3 3
conv5_4: 512 512 3 3
fc6: 1 1 25088 4096
fc7: 1 1 4096 4096
fc8: 1 1 4096 1000
Setting up style layer  	2	:	relu1_1	
Setting up style layer  	7	:	relu2_1	
Setting up style layer  	12	:	relu3_1	
Setting up style layer  	21	:	relu4_1	
Setting up content layer	23	:	relu4_2	
Setting up style layer  	30	:	relu5_1	
Capturing content targets	
nn.Sequential {
  [input -> (1) -> (2) -> (3) -> (4) -> (5) -> (6) -> (7) -> (8) -> (9) -> (10) -> (11) -> (12) -> (13) -> (14) -> (15) -> (16) -> (17) -> (18) -> (19) -> (20) -> (21) -> (22) -> (23) -> (24) -> (25) -> (26) -> (27) -> (28) -> (29) -> (30) -> (31) -> (32) -> (33) -> (34) -> (35) -> (36) -> (37) -> output]
  (1): nn.TVLoss
  (2): nn.SpatialConvolution(3 -> 64, 3x3, 1,1, 1,1)
  (3): nn.ReLU
  (4): nn.StyleLoss
  (5): nn.SpatialConvolution(64 -> 64, 3x3, 1,1, 1,1)
  (6): nn.ReLU
  (7): nn.SpatialMaxPooling(2x2, 2,2)
  (8): nn.SpatialConvolution(64 -> 128, 3x3, 1,1, 1,1)
  (9): nn.ReLU
  (10): nn.StyleLoss
  (11): nn.SpatialConvolution(128 -> 128, 3x3, 1,1, 1,1)
  (12): nn.ReLU
  (13): nn.SpatialMaxPooling(2x2, 2,2)
  (14): nn.SpatialConvolution(128 -> 256, 3x3, 1,1, 1,1)
  (15): nn.ReLU
  (16): nn.StyleLoss
  (17): nn.SpatialConvolution(256 -> 256, 3x3, 1,1, 1,1)
  (18): nn.ReLU
  (19): nn.SpatialConvolution(256 -> 256, 3x3, 1,1, 1,1)
  (20): nn.ReLU
  (21): nn.SpatialConvolution(256 -> 256, 3x3, 1,1, 1,1)
  (22): nn.ReLU
  (23): nn.SpatialMaxPooling(2x2, 2,2)
  (24): nn.SpatialConvolution(256 -> 512, 3x3, 1,1, 1,1)
  (25): nn.ReLU
  (26): nn.StyleLoss
  (27): nn.SpatialConvolution(512 -> 512, 3x3, 1,1, 1,1)
  (28): nn.ReLU
  (29): nn.ContentLoss
  (30): nn.SpatialConvolution(512 -> 512, 3x3, 1,1, 1,1)
  (31): nn.ReLU
  (32): nn.SpatialConvolution(512 -> 512, 3x3, 1,1, 1,1)
  (33): nn.ReLU
  (34): nn.SpatialMaxPooling(2x2, 2,2)
  (35): nn.SpatialConvolution(512 -> 512, 3x3, 1,1, 1,1)
  (36): nn.ReLU
  (37): nn.StyleLoss
}
Capturing style target 1	
Running optimization with L-BFGS	
Iteration 1 / 1000	
  Content 1 loss: 2091176.875000	
  Style 1 loss: 30034.045410	
  Style 2 loss: 701284.033203	
  Style 3 loss: 153918.786621	
  Style 4 loss: 12444803.125000	
  Style 5 loss: 658.482790	
  Total loss: 15421875.348024	
<optim.lbfgs> 	creating recyclable direction/step/history buffers	
Iteration 2 / 1000	
  Content 1 loss: 2091175.625000	
  Style 1 loss: 30034.045410	
  Style 2 loss: 701284.130859	
  Style 3 loss: 153918.774414	
  Style 4 loss: 12444802.343750	
  Style 5 loss: 658.482742	
  Total loss: 15421873.402176
```
