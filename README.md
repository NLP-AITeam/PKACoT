# Source Code of PKACoT for Multimodal Entity and Relation Extraction
Official Implementation of our Paper（PKACoT: Leveraging Chain-of-Thought and Augmented Knowledge via Information Bottleneck for Multimodal Entity and Relation Extraction (Authors:  Wei She, Yongkang Yang, Lihong Zhong, Bin Wang and Wei Liu).

## Required Environment
To run the codes, you need to install the requirements for NER or RE. 
```
transformers==4.11.3
tensorboardX==2.4
TorchCRF==1.1.0
wandb==0.12.1
torchvision==0.8.2
torch==1.7.1
scikit-learn==1.0
seqeval==1.2.2
```

## Model Training
The data path and GPU-related configuration are in the `run.py`. To train the NER model, run this script:

```shell
python -u run.py \
	--dataset_name='twitter15/17'\
	--bert_name="bert-large-uncased"\
	--num_epochs=30\
	--eval_begin_epoch=12\
	--batch_size=12\
	--lr=3e-5\
	--warmup_ratio=0.01\
	--seed = 1234\
	--do_train\
	--ignore_idx=0\
	--max_seq=70\
	--sample_ratio=1.0\
	--save_path="your_ner_ckpt_path"
```

To train the RE model, run this script:

```shell
python run.py \
      --ckpt='your_re_ckpt_path' \
      --max_epoch=20 \
      --batch_size=16 \
      --lr=1e-5 \
      --sample_ratio=1.0
```

## Model Testing
To test the NER model, you can set `load_path` to the trained model path, then run the following script:

```shell
python -u run.py \
      --dataset_name="twitter15/twitter17" \
      --bert_name="bert-large-uncased" \
      --only_test \
      --max_seq=70 \
      --sample_ratio=1.0 \
      --load_path='your_ner_ckpt_path'
```

The settings are similar for RE testing:


```shell
python run.py \
      --ckpt='your_re_ckpt_path' \
      --max_epoch=20 \
      --batch_size=16 \
      --lr=1e-5 \
      --only_test \
      --sample_ratio=1.0 \
```



