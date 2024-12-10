# PEAN
code implementation for paper: [A Novel Multimodal Deep Learning Framework for Encrypted Traffic Classification](https://ieeexplore.ieee.org/abstract/document/9931999)

**If you find this method helpful for your research, please cite this paper:**

```
@article{lin2022novel,
  title={A Novel Multimodal Deep Learning Framework for Encrypted Traffic Classification},
  author={Lin, Peng and Ye, Kejiang and Hu, Yishen and Lin, Yanying and Xu, Cheng-Zhong},
  journal={IEEE/ACM Transactions on Networking},
  year={2022},
  publisher={IEEE},
  volume={},
  number={},
  pages={1-16},
  doi={10.1109/TNET.2022.3215507}
}
```

## Requirements
- Pytorch=1.2.0
- torchvision=0.2.0
- cudatoolkit=10.0
- python 3.6
- transformers=3.0.2 (refer to: [huggingface/transformers](https://github.com/huggingface/transformers))

## Project Structure
After you run PEAN model, your directory structure should be like this:
```
../PEAN
|-- Config
|   |-- pretrain_config.json
|   `-- vocab.txt
|-- DataCache (Generated)
|   `-- sni_whs_10_400_10.txt  (data cache, for easily rerun model at next time)
|-- Model (Generated)
|   |-- log 
|   |-- loss
|   |-- pretrain (where the pretrained model is saved)
|   |-- record
|   `-- save (where the model is saved)
|-- TrafficData
|   |-- class.txt
|   |-- pretrain_test.txt
|   |-- pretrain_train.txt
|   `-- sni_whs_train.txt
|-- PEAN_model.py (core code for PEAN model)
|-- TRF.py        (an implementation of transformer)
|-- config.py     (config for PEAN)
|-- main.py       (main file to run the model)
|-- pretrain.py   (pretrian code)
|-- train_eval.py (implementation of training and eval)
`-- utils.py      (utils)
```

## Quick Start
- The quickest way to use PEAN is (raw bytes + length sequence + improved loss): 
```shell
cd ./PEAN
python main.py --imploss True
```
- Only use bytes
```shell
cd ./PEAN
python main.py --feature raw
```
- Only use length sequence
```shell
cd ./PEAN
python main.py --feature length
```
- Change the packet number (default: 10)
```shell
cd ./PEAN
python main.py --pad_num 12 --pad_len_seq 12
```
- Change the byte number (default: 400)
```shell
cd ./PEAN
python main.py --pad_len 500
```
- if you want to pretrain, you must first:;
```shell
cd ./PEAN
python pretrain.py
```
and then: 
```shell
python main.py --embway pretrain --imploss True
```
