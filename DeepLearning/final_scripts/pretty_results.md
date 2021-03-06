## Parameters: 

```
DATA_FILE="../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv"
TEST_FILE="../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv"
EMB_FILE="../../../0_embeddings/glove.6B/glove.6B.300d.txt" #options: {50,100,200,300}d
MODEL_NAME="modelKeras"
MODEL_TYPE='BiLSTM2_CNN3_model'
PREPROC="remove_stopwords_and_punctuation_textblob"

VOCAB_SIZE=7500
EMBEDDING_DIM=300
MAX_LENGTH=64
TRUNC_TYPE="post"
PADDING_TYPE="post"
OOV_TOK="<OOV>"
TRAINING_PORTION=0.8
NUM_EPOCHS=50
LSTM_OUT=32
NUM_FILTERS=16
DROPOUT=0.5
KERNEL_SIZE=3
STRIDES=1
LEARNING_RATE=0.001 #0.001
VERBOSE=1
POOL_SIZE=2
```

- models: 
```
	parser.add_argument("model_type", metavar="MODEL_TYPE", 
		choices=['basic_model', 'LSTM_model', 'LSTM_model2', 
		'BiLSTM_model', 'BiLSTM_short_model',
		'BiLSTM_moreReg_model', 'BiLSTM_moreReg_model2',
		'BiLSTM_CNN_model', 'CNN_model', 'BiLSTM2_model',
		'BiLSTM2_CNN_model', 'BiLSTM2_CNN3_model', 
		'BiLSTM2_CNN3_short_model', 'BiLSTM2_CNN3_supershort_model'])
```

- Early stopping: **Patience = 15**, val_f1

### Basic no emb <--
3. Accs through 3 runs: 
	- test acc: 0.7709, 0.7012, 0.6965
	- test f1: 0.5155, 0.4838, 0.5064
	- mtsa acc: 

### Basic model <--

1. Structure: 
		-  emb -> global avg pool 1d -> dense(24) -> dense(1)
2. Results: 
		- Epoch [19]: val_f1 did not improve from: 0.63556
		- **val:** `loss: 0.5576 - acc: 0.7700 - rec: 0.5809 - prec: 0.6734 - f1: 0.6141`
		- **test:** `loss: 0.6155 - acc: 0.7407 - rec: 0.6142 - prec: 0.5392 - f1: 0.5576`
3. Accs through 3 runs: 
	- test acc: 0.7407, 0.7837, 0.7326 
	- test f1: 0.5576, 0.5436, 0.5473

## LSTM model 

1. Structure: 
		-  emb -> spatial dropout 1d -> LSTM -> dense(24) -> dense(1)
2. Results: 
		- Epoch [16]: val_f1 did not improve from: 0.00000
		- **val:** `loss: 0.6350 - acc: 0.6688 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00`
		- **test:** `loss: 0.5976 - acc: 0.7209 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00`

## LSTM model2

1. Structure: 
		- emb -> LSTM -> dense(24) -> dense(1)
2. Results: 
		- Epoch [16]: val_f1 did not improve from: 0.00000
		- **val:** `loss: 0.6350 - acc: 0.6688 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00`
		- **test:** `loss: 0.5982 - acc: 0.7209 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00`


## BiLSTM model <-- 

1. Structure: 
		- emb -> dropout -> biLSTM -> dense(64) -> dense(32) -> dense(1)
2. Results: 
		- Epoch [17]: val_f1 did not improve from: 0.63016
		- **val:** `loss: 0.4650 - acc: 0.7946 - rec: 0.5665 - prec: 0.7542 - f1: 0.6344`
		- **test:** `loss: 0.4162 - acc: 0.8326 - rec: 0.4749 - prec: 0.8272 - f1: 0.5897`
3. Accs through 3 runs: 
	- test acc: 0.8326, 0.8302, 0.8233
	- test f1: 0.5897, 0.5871, 0.6148

## BiLSTM short model

1. Structure: 
		- emb -> dropout -> biLSTM -> dense(1)
2. Results: 
		- Epoch [18]: val_f1 did not improve from: 0.63556
		- **val:** `loss: 0.4768 - acc: 0.7855 - rec: 0.6011 - prec: 0.7067 - f1: 0.6377`
		- **test:** `loss: 0.4257 - acc: 0.8221 - rec: 0.5211 - prec: 0.7378 - f1: 0.5968`


## BiLSTM moreReg model

1. Structure: 
		- emb -> dropout -> BiLSTM(+dropout) -> dense(64) -> dense(32) -> dense(1)
2. Results: 
		- Epoch [19]: val_f1 did not improve from: 0.66122
		- **val:** `loss: 0.4865 - acc: 0.7817 - rec: 0.6726 - prec: 0.6748 - f1: 0.6629`
		- **test:** `loss: 0.4649 - acc: 0.7942 - rec: 0.6743 - prec: 0.6133 - f1: 0.6332`


## BiLSTM moreReg model2

1. Structure: 
		- emb -> dropout -> BiLSTM(+dropout) -> dense(64) -> dense(32) -> dense(1)
2. Results: 
		- Epoch [18]: val_f1 did not improve from: 0.65633
		- **val:** `loss: 0.4702 - acc: 0.7870 - rec: 0.6340 - prec: 0.6921 - f1: 0.6513`
		- **test:** `loss: 0.4379 - acc: 0.8302 - rec: 0.5854 - prec: 0.7532 - f1: 0.6441`

## CNN model <--

1. Structure: 
		- emb -> dropout -> conv1d -> global_max_pool_1d -> dense(250) -> dropout -> dense(1)
2. Results filters = 16: 
		- Epoch [21]: val_f1 did not improve from: 0.61153
		- **val:** `loss: 0.6756 - acc: 0.7466 - rec: 0.6143 - prec: 0.6158 - f1: 0.6046`
		- **test:** `loss: 0.9280 - acc: 0.6872 - rec: 0.6679 - prec: 0.4710 - f1: 0.5353`
2. Results filters = 32: 
		- Epoch [19]: val_f1 did not improve from: 0.61283
		- **val:** `loss: 0.5594 - acc: 0.7693 - rec: 0.5700 - prec: 0.6736 - f1: 0.6079`
		- **test:** `loss: 0.5820 - acc: 0.7628 - rec: 0.5248 - prec: 0.5882 - f1: 0.5425`
2. Results filters = 64: 
		- Epoch [18]: val_f1 did not improve from: 0.63279
		- **val:** `loss: 0.5288 - acc: 0.7704 - rec: 0.6181 - prec: 0.6628 - f1: 0.6303`
		- **test:** `loss: 0.5145 - acc: 0.7674 - rec: 0.5582 - prec: 0.5790 - f1: 0.5582`
3. Accs through 3 runs: 
	- CNN 16: 
		- test acc: 0.7000,  0.7988, 0.7256
		- test f1: 0.5635, 0.5977, 0.5452
	- CNN 64: 
		- test acc: 0.7349, 0.6907, 0.7523
		- test f1: 0.5382, 0.5602, 0.5451
	- CNN 256: 
		- test acc: 0.7326, 0.7698, 0.7547
		- test f1: 0.5583, 0.5696, 0.5804

## BiLSTM CNN model <-- 

1. Structure: 
		- emb -> dropout -> BiLSTM(+dropout) -> dense(128) -> dense(32) -> dense(1)
		- 				\-> conv1d -> GMpool -/
2. Results: 
		- Epoch [19]: val_f1 did not improve from: from 0.65768
		- **val:** `loss: 0.4822 - acc: 0.7889 - rec: 0.6355 - prec: 0.6991 - f1: 0.6558`
		- **test:** `loss: 0.4328 - acc: 0.8233 - rec: 0.6417 - prec: 0.6821 - f1: 0.6461`
3. Accs through 3 runs: 
	- test acc: 0.8233, 0.8267, 0.8140
	- test f1: 0.6461, 0.6130, 0.6418

## BiLSTM2 CNN model

1. Structure: 
		- emb -> dropout -> BiLSTM(+dropout) -> dropout -> BiLSTM(+dropout)-> dense(128) -> dense(32) -> dense(1)
		- 				\-> conv1d -> global max pool 1d ------------------/
2. Results: 
		- Epoch [22]: val_f1 did not improve from: from 0.64637
		- **val:** `loss: 0.5739 - acc: 0.7636 - rec: 0.6847 - prec: 0.6284 - f1: 0.6439`
		- **test:** `loss: 0.4843 - acc: 0.7849 - rec: 0.7196 - prec: 0.5901 - f1: 0.6357`

## BiLSTM2 CNN3 model <-- 

1. Structure: 
		- emb -> dropout -> BiLSTM(+dropout) -> dropout -> BiLSTM(+dropout)-> dense(512) -> dropout -> dense(128) -> dropout -> dense(32) -> dense(1)
		- 				\-> conv1d -> global max pool 1d ------------------/
		- 				\-> conv1d -> global max pool 1d ------------------/
		- 				\-> conv1d -> global max pool 1d ------------------/
2. Results: 
		- Epoch [20]: val_f1 did not improve from: from 0.65814
		- **val:** `loss: 0.5116 - acc: 0.7761 - rec: 0.6835 - prec: 0.6562 - f1: 0.6606`
		- **test:** `loss: 0.4250 - acc: 0.8070 - rec: 0.6367 - prec: 0.6436 - f1: 0.6311`
3. Accs through 3 runs: 
	- test acc: 0.8070, 0.8395, 0.7988
	- test f1: 0.6311, 0.6778, 0.6239

## BiLSTM2 CNN short model <-- 

1. Structure: 
		- emb -> dropout -> BiLSTM(+dropout) -> dropout -> BiLSTM(+dropout)-> dropout -> dense(32) -> dense(1)
		- 				\-> conv1d -> global max pool 1d ------------------/
		- 				\-> conv1d -> global max pool 1d ------------------/
		- 				\-> conv1d -> global max pool 1d ------------------/
2. Results **lstm_out=32, num_filters = 16, lr = 0.001**: 
		- Epoch [18]: val_f1 did not improve from: from 0.65417
		- **val:** `loss: 0.4786 - acc: 0.7900 - rec: 0.6327 - prec: 0.7019 - f1: 0.6541`
		- **test:** `loss: 0.4248 - acc: 0.8302 - rec: 0.5047 - prec: 0.7900 - f1: 0.5948`
3. Results **lstm_out=32, num_filters = 32, lr = 0.001**: 
		- Epoch [21]: val_f1 did not improve from: 0.65580
		- **val:** `loss: 0.4712 - acc: 0.7931 - rec: 0.6253 - prec: 0.7219 - f1: 0.6595`
		- **test:** `loss: 0.4281 - acc: 0.8337 - rec: 0.4976 - prec: 0.8268 - f1: 0.6032`
4. Results **lstm_out=64, num_filters = 64, lr = 0.001**: 
		- Epoch [22]: val_f1 did not improve from: 0.65145
		- **val:** `loss: 0.4833 - acc: 0.7783 - rec: 0.6738 - prec: 0.6638 - f1: 0.6590`
		- **test:** `loss: 0.4283 - acc: 0.8163 - rec: 0.6660 - prec: 0.6738 - f1: 0.6567`
5. Results **lstm_out=64, num_filters = 16, lr = 0.001**: 
		- Epoch [20]: val_f1 did not improve from: 0.65929
		- **val:** `loss: 0.5067 - acc: 0.7772 - rec: 0.6888 - prec: 0.6570 - f1: 0.6628`
		- **test:** `loss: 0.4575 - acc: 0.7930 - rec: 0.6545 - prec: 0.6172 - f1: 0.6226`
6. Results **lstm_out=64, num_filters = 16, lr = 0.0001**: 
		- Epoch [30]: val_f1 did not improve from: 0.65957
		- **val:** `loss: 0.4712 - acc: 0.7931 - rec: 0.6253 - prec: 0.7219 - f1: 0.6595`
		- **test:** `loss: 0.4281 - acc: 0.8337 - rec: 0.4976 - prec: 0.8268 - f1: 0.6032`
7. Accs through 3 runs: **lstm_out=32, num_filters = 16, lr = 0.001**
	- test acc:  0.8302, 
	- test f1: 0.5948
8. Accs through 3 runs: **lstm_out=64, num_filters = 64, lr = 0.001**
	- test acc: 0.8163, 0.8326, 0.8326
	- test f1: 0.6567, 0.6503, 0.6222

## BiLSTM2 CNN supershort model

1. Structure: 
		- emb -> dropout -> BiLSTM(+dropout) -> dropout -> BiLSTM(+dropout)-> dropout -> dense(1)
		- 				\-> conv1d -> global max pool 1d ------------------/
		- 				\-> conv1d -> global max pool 1d ------------------/
		- 				\-> conv1d -> global max pool 1d ------------------/
2. Results **lstm_out=32, num_filters=16**: 
		- Epoch [17]: val_f1 did not improve from: 0.65606
		- **val:** `loss: 0.4600 - acc: 0.7953 - rec: 0.6003 - prec: 0.7337 - f1: 0.6491`
		- **test:** `loss: 0.4178 - acc: 0.8349 - rec: 0.4979 - prec: 0.8273 - f1: 0.6111`


