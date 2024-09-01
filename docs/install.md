# installation

Detailed package versions can be found in [requirements.txt](../requirements.txt).



**a. Create a conda virtual environment and activate it.**
```shell
conda create -n genad python=3.8 -y
conda activate genad
```

**b. Install PyTorch and torchvision following the [official instructions](https://pytorch.org/).**
```shell
pip install torch==1.9.1+cu111 torchvision==0.10.1+cu111 torchaudio==0.9.1 -f https://download.pytorch.org/whl/torch_stable.html
# Recommended torch>=1.9
```

**c. Install gcc>=5 in conda env (optional).**
```shell
conda install -c omgarcia gcc-5 # gcc-6.2
```

**c. Install mmcv-full.**
```shell
pip install mmcv-full==1.4.0
#  pip install mmcv-full==1.4.0 -f https://download.openmmlab.com/mmcv/dist/cu111/torch1.9.0/index.html
```

**d. Install mmdet and mmseg.**
```shell
pip install mmdet==2.14.0
pip install mmsegmentation==0.14.1
```

**e. Install timm.**
```shell
pip install timm
```

**f. Install mmdet3d.**
```shell
conda activate genad
git clone https://github.com/open-mmlab/mmdetection3d.git
cd /path/to/mmdetection3d
git checkout -f v0.17.1
python setup.py develop
```
或
```shell
CXX=g++-9 CC=gcc-9 LD=g++-9 pip install -e .
```

答案来自 https://stackoverflow.com/questions/72009245/subprocess-calledprocesserror-command-which-c-returned-non-zero-exit

在训练的时候有个问题：AttributeError:module ‘distutils‘ has no attribute ‘version

这个时候去环境里看一下setuptools的版本，问题可能出在setuptools的版本过高。直接安装即可：

```shell
pip install setuptools==59.5.0
```

答案来自https://blog.csdn.net/qq_45783225/article/details/129191110

运行报错
```shell
WARNING:__main__:*****************************************
Setting OMP_NUM_THREADS environment variable for each process to be 1 in default, to avoid your system being overloaded, please further tune the variable for optimal performance in your application as needed. 
*****************************************
projects.mmdet3d_plugin
projects.mmdet3d_plugin
Traceback (most recent call last):
  File "tools/train.py", line 321, in <module>
    main()
  File "tools/train.py", line 180, in main
    cfg.dump(osp.join(cfg.work_dir, osp.basename(args.config)))
  File "/root/anaconda3/envs/genad/lib/python3.8/site-packages/mmcv/utils/config.py", line 541, in dump
    f.write(self.pretty_text)
  File "/root/anaconda3/envs/genad/lib/python3.8/site-packages/mmcv/utils/config.py", line 496, in pretty_text
    text, _ = FormatCode(text, style_config=yapf_style, verify=True)Traceback (most recent call last):

  File "tools/train.py", line 321, in <module>
TypeError: FormatCode() got an unexpected keyword argument 'verify'
    main()
  File "tools/train.py", line 180, in main
    cfg.dump(osp.join(cfg.work_dir, osp.basename(args.config)))
  File "/root/anaconda3/envs/genad/lib/python3.8/site-packages/mmcv/utils/config.py", line 541, in dump
    f.write(self.pretty_text)
  File "/root/anaconda3/envs/genad/lib/python3.8/site-packages/mmcv/utils/config.py", line 496, in pretty_text
    text, _ = FormatCode(text, style_config=yapf_style, verify=True)
TypeError: FormatCode() got an unexpected keyword argument 'verify'
```

根据 https://blog.csdn.net/ZZZZ_Y_/article/details/133902230

```shell
pip uninstall yapf
pip install yapf==0.40.1
```

**g. Install nuscenes-devkit.**
```shell
pip install nuscenes-devkit==1.1.9
```

**h. Clone GenAD.**
```shell
git clone https://github.com/wzzheng/GenAD.git
```

**i. Prepare pretrained models.**
```shell
cd /path/to/GenAD
mkdir ckpts
cd ckpts 
wget https://download.pytorch.org/models/resnet50-19c8e357.pth
```

**j. 进行测试前.**
pip install similaritymeasures

