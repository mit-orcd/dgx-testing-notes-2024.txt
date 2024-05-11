### Login
      ssh -A -l cnh eofe7.mit.edu
      ssh -A nvidia-bcm

      cd   /home/cnh/
      mkdir myenv
      cd /home/cnh/myenv
      wget https://repo.anaconda.com/miniconda/Miniconda3-py312_24.3.0-0-Linux-x86_64.sh
      chmod +x Miniconda3-py312_24.3.0-0-Linux-x86_64.sh
      ./Miniconda3-py312_24.3.0-0-Linux-x86_64.sh -p mc3 -b
      . mc3/bin/activate
      conda create -n vila python=3.10 -y
      source activate vila
      pip install --upgrade pip
      conda install -c nvidia cuda-toolkit -y
      wget https://github.com/Dao-AILab/flash-attention/releases/download/v2.5.8/flash_attn-2.5.8+cu122torch2.3cxx11abiFALSE-cp310-cp310-linux_x86_64.whl
      pip install flash_attn-2.5.8+cu122torch2.3cxx11abiFALSE-cp310-cp310-linux_x86_64.whl
      git clone https://github.com/kentang-mit/VILA-h100
      cd VILA-h100/
      pip install -e .
      pip install -e ".[train]"
      pip install git+https://github.com/huggingface/transformers@v4.36.2
      site_pkg_path=$(python -c 'import site; print(site.getsitepackages()[0])') && cp -rv ./llava/train/transformers_replace/* $site_pkg_path/transformers/

       ssh dgx-01

       cd /raid/cnh
       source ~/myenv/mc3/bin/activate
       source activate vila
       python <<!
       import torch
       import transformers
       import flash_attn
       import deepspeed
       !


