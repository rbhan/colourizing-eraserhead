# Install neural-style on OS X Mavericks (https://github.com/jcjohnson/neural-style)

## Install torch and lua

In terminal:

$ git clone https://github.com/torch/distro.git ~/torch --recursive
$ cd ~/torch; bash install-deps; # installs package dependencies
$ ./install.sh # installs LuaJIT, Lua Rocks

$ cat .bash_profile >> .profile 
$ rm .bash_profile
$ source ~/.profile # adds torch to PATH

To remove torch: 
$ rm -rf ~/torch

Run torch from terminal:
$ th

Install with luarocks:
$ luarocks install torch
$ luarocks install nn
$ luarocks install optim
$ luarocks install lua-cjson

Install torch-hdf5 from GitHub:
$ git clone https://github.com/deepmind/torch-hdf5
$ cd torch-hdf5
$ luarocks make hdf5-0-0.rockspec

## Install loadcaffe

$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" # installs Homebrew
$ brew install libprotobuf-dev protobuf-compiler # Google protocal buffer library
$ luarocks install loadcaffe

# Install neural-style
