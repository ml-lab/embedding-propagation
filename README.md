## Embedding Propagation: Smoother Manifold for Few-Shot Classification 
[[Paper](https://arxiv.org/abs/2003.04151)]

![](embedding_prop.jpeg)

## Usage
```python
import torch
from src.modules.embedding_propagation import EmbeddingPropagation

ep = EmbeddingPropagation()
features = torch.randn(32, 32)
embeddings = ep(features)
```

## Data
* [mini-imagenet](https://github.com/renmengye/few-shot-ssl-public#miniimagenet) ([pre-processing](https://github.com/ElementAI/TADAM/tree/master/datasets))
* [tiered-imagenet](https://github.com/renmengye/few-shot-ssl-public#tieredimagenet)
* [CUB](https://github.com/wyharveychen/CloserLookFewShot/tree/master/filelists/CUB)

You can either edit `data_root` in the `exp_configs/[pretraining|finetuning].py` or create a symbolic link to the each of the dataset folders at `./data/dataset-name/` (default).

## Reproducing results in the paper
1. Pre-train the models: `python3 trainval.py -e pretrain -sb ./logs/pretraining`
2. Edit `exp_configs/finetune_exps.py`. Set `"pretrained_weights_root": ./logs/pretraining/`
3. Fine-tune: `python3 trainval.py -e finetune -sb ./logs`

## Results
|support_size|dataset_train|backbone|test_accuracy|test_confidence|
|:----------------:|:-----------:|:------:|:-----------:|:-------------:|
|        1         |     cub     | conv4  |   0.6692    |    0.0094     |
|        1         |     cub     |resnet12|   0.8285    |    0.0081     |
|        1         |     cub     |  wrn   |   0.8775    |    0.0070     |
|        1         |miniimagenet | conv4  |   0.5932    |    0.0084     |
|        1         |miniimagenet |resnet12|   0.6837    |    0.0086     |
|        1         |miniimagenet |  wrn   |   0.7074    |    0.0086     |
|        1         |tiered-imagen| conv4  |   0.6070    |    0.0097     |
|        1         |tiered-imagen|resnet12|   0.7677    |    0.0085     |
|        1         |tiered-imagen|  wrn   |   0.7850    |    0.0086     |
|                  |             |        |             |               |
|        5         |     cub     | conv4  |   0.7984    |    0.0067     |
|        5         |     cub     |resnet12|   0.9132    |    0.0042     |
|        5         |     cub     |  wrn   |   0.9404    |    0.0036     |
|        5         |miniimagenet | conv4  |   0.7295    |    0.0063     |
|        5         |miniimagenet |resnet12|   0.8152    |    0.0058     |
|        5         |miniimagenet |  wrn   |   0.8434    |    0.0056     |
|        5         |tiered-imagen| conv4  |   0.7391    |    0.0074     |
|        5         |tiered-imagen|resnet12|   0.8748    |    0.0058     |
|        5         |tiered-imagen|  wrn   |   0.8845    |    0.0053     |

## Cite
```
@article{rodriguez2020embedding,
  title={Embedding Propagation: Smoother Manifold for Few-Shot Classification},
  author={Pau Rodríguez and Issam Laradji and Alexandre Drouin and Alexandre Lacoste},
  year={2020},
  journal={arXiv preprint arXiv:2003.04151},
}
```
