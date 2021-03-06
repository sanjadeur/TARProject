
	parser.add_argument("model_type", metavar="MODEL_TYPE", 
		choices=['basic_model', 'LSTM_model', 'LSTM_model2', 
		'BiLSTM_model', 'BiLSTM_short_model',
		'BiLSTM_moreReg_model', 'BiLSTM_moreReg_model2',
		'BiLSTM_CNN_model', 'CNN_model', 'BiLSTM2_model',
		'BiLSTM2_CNN_model', 'BiLSTM2_CNN3_model', 
		'BiLSTM2_CNN3_short_model', 'BiLSTM2_CNN3_supershort_model'])

**Params:**
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

```
=============================================
        BiLSTM2_CNN3_supershort_model
=============================================

Model: "model"
__________________________________________________________________________________________________
Layer (type)                    Output Shape         Param #     Connected to
==================================================================================================
input_1 (InputLayer)            [(None, 64)]         0
__________________________________________________________________________________________________
embedding (Embedding)           (None, 64, 300)      2250000     input_1[0][0]
__________________________________________________________________________________________________
bidirectional (Bidirectional)   (None, 64, 128)      186880      embedding[0][0]
__________________________________________________________________________________________________
conv1d (Conv1D)                 (None, 62, 32)       28832       embedding[0][0]
__________________________________________________________________________________________________
conv1d_1 (Conv1D)               (None, 61, 32)       38432       embedding[0][0]
__________________________________________________________________________________________________
conv1d_2 (Conv1D)               (None, 60, 32)       48032       embedding[0][0]
__________________________________________________________________________________________________
dropout (Dropout)               (None, 64, 128)      0           bidirectional[0][0]
__________________________________________________________________________________________________
global_max_pooling1d (GlobalMax (None, 32)           0           conv1d[0][0]
__________________________________________________________________________________________________
global_max_pooling1d_1 (GlobalM (None, 32)           0           conv1d_1[0][0]
__________________________________________________________________________________________________
global_max_pooling1d_2 (GlobalM (None, 32)           0           conv1d_2[0][0]
__________________________________________________________________________________________________
bidirectional_1 (Bidirectional) (None, 128)          98816       dropout[0][0]
__________________________________________________________________________________________________
concatenate (Concatenate)       (None, 224)          0           global_max_pooling1d[0][0]
                                                                 global_max_pooling1d_1[0][0]
                                                                 global_max_pooling1d_2[0][0]
                                                                 bidirectional_1[0][0]
__________________________________________________________________________________________________
dropout_1 (Dropout)             (None, 224)          0           concatenate[0][0]
__________________________________________________________________________________________________
dense (Dense)                   (None, 1)            225         dropout_1[0][0]
==================================================================================================
Total params: 2,651,217
Trainable params: 2,651,217
Non-trainable params: 0
__________________________________________________________________________________________________
Train on 10592 samples, validate on 2648 samples
Epoch 1/50
```



### Preproc: remove_stopwords_and_punctuation_textblob


#### Svi modeli sa slicnim parametrima

---

- basic model:
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.0941 - acc: 0.9656 - rec: 0.9404 - prec: 0.9545 - f1: 0.9442
Epoch 00019: val_f1 did not improve from 0.61472

10592/10592 [==============================] - 14s 1ms/sample - loss: 0.0940 - acc: 0.9657 - rec: 0.9404 - prec: 0.9548 - f1: 0.9444 - val_loss: 1.5763 - val_acc: 0.7054 - val_rec: 0.5964 - val_prec: 0.5477 - val_f1: 0.5604
Epoch 00019: early stopping

2648/2648 [==============================] - 0s 72us/sample - loss: 1.5763 - acc: 0.7054 - rec: 0.5952 - prec: 0.5504 - f1: 0.5615

SCORES:
[1.5763122001803533, 0.7054381, 0.59517336, 0.5503734, 0.5615056]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='basic_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 93us/sample - loss: 0.5576 - acc: 0.7700 - rec: 0.5809 - prec: 0.6734 - f1: 0.6141
[0.5576225015872195, 0.7700151, 0.58089054, 0.67337257, 0.6141437]

Scores on test:
860/860 [==============================] - 0s 70us/sample - loss: 0.6155 - acc: 0.7407 - rec: 0.6142 - prec: 0.5392 - f1: 0.5576
[0.6154905467532402, 0.7406977, 0.61419004, 0.5392118, 0.5575645]

```


- LSTM model: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.6366 - acc: 0.6673 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00
Epoch 00016: val_f1 did not improve from 0.00000

10592/10592 [==============================] - 63s 6ms/sample - loss: 0.6365 - acc: 0.6674 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00 - val_loss: 0.6352 - val_acc: 0.6688 - val_rec: 0.0000e+00 - val_prec: 0.0000e+00 - val_f1: 0.0000e+00
Epoch 00016: early stopping

2648/2648 [==============================] - 2s 891us/sample - loss: 0.6352 - acc: 0.6688 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00

SCORES:
[0.6352207379758898, 0.6688067, 0.0, 0.0, 0.0]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='LSTM_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 3s 1ms/sample - loss: 0.6350 - acc: 0.6688 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00
[0.6350448430484875, 0.6688067, 0.0, 0.0, 0.0]

Scores on test:
860/860 [==============================] - 1s 668us/sample - loss: 0.5976 - acc: 0.7209 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00
[0.5976139010385025, 0.7209302, 0.0, 0.0, 0.0]

```

- LSTM_model2
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.6365 - acc: 0.6673 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00
Epoch 00016: val_f1 did not improve from 0.00000

10592/10592 [==============================] - 31s 3ms/sample - loss: 0.6364 - acc: 0.6674 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00 - val_loss: 0.6351 - val_acc: 0.6688 - val_rec: 0.0000e+00 - val_prec: 0.0000e+00 - val_f1: 0.0000e+00
Epoch 00016: early stopping

2648/2648 [==============================] - 1s 407us/sample - loss: 0.6351 - acc: 0.6688 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00

SCORES:
[0.6350585310480746, 0.6688067, 0.0, 0.0, 0.0]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='LSTM_model2', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 3s 1ms/sample - loss: 0.6350 - acc: 0.6688 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00
[0.6350238249381143, 0.6688067, 0.0, 0.0, 0.0]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.5982 - acc: 0.7209 - rec: 0.0000e+00 - prec: 0.0000e+00 - f1: 0.0000e+00
[0.598183247654937, 0.7209302, 0.0, 0.0, 0.0]

```

- BiLSTM_model
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0695 - acc: 0.9740 - rec: 0.9509 - prec: 0.9703 - f1: 0.9580
Epoch 00017: val_f1 did not improve from 0.63016

10592/10592 [==============================] - 72s 7ms/sample - loss: 0.0693 - acc: 0.9740 - rec: 0.9510 - prec: 0.9704 - f1: 0.9581 - val_loss: 1.4243 - val_acc: 0.7390 - val_rec: 0.5657 - val_prec: 0.6076 - val_f1: 0.5762
Epoch 00017: early stopping

2648/2648 [==============================] - 3s 984us/sample - loss: 1.4243 - acc: 0.7390 - rec: 0.5656 - prec: 0.6071 - f1: 0.5770

SCORES:
[1.4243092925887093, 0.73904836, 0.56557477, 0.607141, 0.5769856]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 1ms/sample - loss: 0.4650 - acc: 0.7946 - rec: 0.5665 - prec: 0.7542 - f1: 0.6344
[0.46496168166128893, 0.7945619, 0.56645834, 0.75420284, 0.6343891]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4162 - acc: 0.8326 - rec: 0.4749 - prec: 0.8272 - f1: 0.5897
[0.4161978666172471, 0.83255816, 0.474931, 0.8271886, 0.5896847]

```

- BiLSTM_short_model
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0667 - acc: 0.9756 - rec: 0.9599 - prec: 0.9674 - f1: 0.9618
Epoch 00018: val_f1 did not improve from 0.63556

10592/10592 [==============================] - 42s 4ms/sample - loss: 0.0666 - acc: 0.9756 - rec: 0.9601 - prec: 0.9675 - f1: 0.9619 - val_loss: 1.3583 - val_acc: 0.7349 - val_rec: 0.5478 - val_prec: 0.5995 - val_f1: 0.5607
Epoch 00018: early stopping

2648/2648 [==============================] - 1s 508us/sample - loss: 1.3583 - acc: 0.7349 - rec: 0.5569 - prec: 0.6112 - f1: 0.5702

SCORES:
[1.358320071077779, 0.7348943, 0.55690724, 0.6111958, 0.57016385]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM_short_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 2s 682us/sample - loss: 0.4768 - acc: 0.7855 - rec: 0.6011 - prec: 0.7067 - f1: 0.6377
[0.47680333337755004, 0.7854985, 0.60108334, 0.7066937, 0.6376653]

Scores on test:
860/860 [==============================] - 1s 602us/sample - loss: 0.4257 - acc: 0.8221 - rec: 0.5211 - prec: 0.7378 - f1: 0.5968
[0.42569636640160585, 0.822093, 0.5210896, 0.73780006, 0.59684014]

```

- BiLSTM_moreReg_model
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.0830 - acc: 0.9683 - rec: 0.9456 - prec: 0.9576 - f1: 0.9492
10560/10592 [============================>.] - ETA: 0s - loss: 0.0830 - acc: 0.9683 - rec: 0.9454 - prec: 0.9578 - f1: 0.9492
Epoch 00019: val_f1 did not improve from 0.66122

10592/10592 [==============================] - 55s 5ms/sample - loss: 0.0832 - acc: 0.9682 - rec: 0.9449 - prec: 0.9579 - f1: 0.9490 - val_loss: 1.4884 - val_acc: 0.7447 - val_rec: 0.5470 - val_prec: 0.6391 - val_f1: 0.5757
Epoch 00019: early stopping

2648/2648 [==============================] - 2s 711us/sample - loss: 1.4884 - acc: 0.7447 - rec: 0.5421 - prec: 0.6296 - f1: 0.5701

SCORES:
[1.4883746810910206, 0.744713, 0.54207945, 0.62955856, 0.5700964]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=64, max_len=64, model_name='modelKeras', model_type='BiLSTM_moreReg_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 3s 993us/sample - loss: 0.4865 - acc: 0.7817 - rec: 0.6726 - prec: 0.6748 - f1: 0.6629
[0.48651776546077785, 0.78172207, 0.672598, 0.6747764, 0.6628616]

Scores on test:
860/860 [==============================] - 1s 870us/sample - loss: 0.4649 - acc: 0.7942 - rec: 0.6743 - prec: 0.6133 - f1: 0.6332
[0.4649375625821047, 0.79418606, 0.6743176, 0.6132964, 0.6331512]

```

- BiLSTM_moreReg_model2
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0958 - acc: 0.9634 - rec: 0.9351 - prec: 0.9537 - f1: 0.9413
Epoch 00018: val_f1 did not improve from 0.65633

10592/10592 [==============================] - 80s 8ms/sample - loss: 0.0959 - acc: 0.9633 - rec: 0.9353 - prec: 0.9533 - f1: 0.9412 - val_loss: 1.2018 - val_acc: 0.7390 - val_rec: 0.6185 - val_prec: 0.6040 - val_f1: 0.6014
Epoch 00018: early stopping

2648/2648 [==============================] - 3s 1ms/sample - loss: 1.2018 - acc: 0.7390 - rec: 0.6099 - prec: 0.6081 - f1: 0.5971

SCORES:
[1.2018214300319867, 0.73904836, 0.60989493, 0.60814875, 0.5971237]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM_moreReg_model2', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 2ms/sample - loss: 0.4702 - acc: 0.7870 - rec: 0.6340 - prec: 0.6921 - f1: 0.6513
[0.4702442585521594, 0.78700906, 0.6340009, 0.6920787, 0.65126616]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4379 - acc: 0.8302 - rec: 0.5854 - prec: 0.7532 - f1: 0.6441
[0.4378574473913326, 0.83023256, 0.5853887, 0.7532336, 0.6441196]

```

- CNN_model filters 16
```
10464/10592 [============================>.] - ETA: 0s - loss: 0.0868 - acc: 0.9687 - rec: 0.9449 - prec: 0.9604 - f1: 0.9493
10528/10592 [============================>.] - ETA: 0s - loss: 0.0867 - acc: 0.9687 - rec: 0.9450 - prec: 0.9604 - f1: 0.9494
Epoch 00021: val_f1 did not improve from 0.61153

10592/10592 [==============================] - 19s 2ms/sample - loss: 0.0869 - acc: 0.9686 - rec: 0.9446 - prec: 0.9607 - f1: 0.9493 - val_loss: 1.8576 - val_acc: 0.7058 - val_rec: 0.5968 - val_prec: 0.5530 - val_f1: 0.5632
Epoch 00021: early stopping

2648/2648 [==============================] - 0s 114us/sample - loss: 1.8576 - acc: 0.7058 - rec: 0.5932 - prec: 0.5498 - f1: 0.5598

SCORES:
[1.8576362612024175, 0.70581573, 0.5931771, 0.54977566, 0.55983293]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='CNN_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 182us/sample - loss: 0.6756 - acc: 0.7466 - rec: 0.6143 - prec: 0.6158 - f1: 0.6046
[0.6755979892170321, 0.7466012, 0.6143097, 0.61577624, 0.60458]

Scores on test:
860/860 [==============================] - 0s 128us/sample - loss: 0.9280 - acc: 0.6872 - rec: 0.6679 - prec: 0.4710 - f1: 0.5353
[0.9280086783475654, 0.6872093, 0.6679301, 0.47095093, 0.53531295]

```

- CNN_model, filters 32
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0926 - acc: 0.9679 - rec: 0.9457 - prec: 0.9563 - f1: 0.9479
Epoch 00019: val_f1 did not improve from 0.61283

10592/10592 [==============================] - 10s 969us/sample - loss: 0.0926 - acc: 0.9680 - rec: 0.9459 - prec: 0.9564 - f1: 0.9481 - val_loss: 1.6415 - val_acc: 0.6934 - val_rec: 0.6167 - val_prec: 0.5298 - val_f1: 0.5603
Epoch 00019: early stopping

2648/2648 [==============================] - 0s 54us/sample - loss: 1.6415 - acc: 0.6934 - rec: 0.6172 - prec: 0.5304 - f1: 0.5598

SCORES:
[1.6414570372630461, 0.6933535, 0.6171638, 0.5304396, 0.559765]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='CNN_model', num_epochs=50, num_filters=32, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 74us/sample - loss: 0.5594 - acc: 0.7693 - rec: 0.5700 - prec: 0.6736 - f1: 0.6079
[0.559427555864311, 0.7692598, 0.5699912, 0.6735545, 0.6078938]

Scores on test:
860/860 [==============================] - 0s 51us/sample - loss: 0.5820 - acc: 0.7628 - rec: 0.5248 - prec: 0.5882 - f1: 0.5425
[0.5820353284824726, 0.7627907, 0.52484506, 0.58819884, 0.5424703]

```

- CNN_model, filters 64
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.0960 - acc: 0.9668 - rec: 0.9430 - prec: 0.9562 - f1: 0.9465
Epoch 00018: val_f1 did not improve from 0.63279

10592/10592 [==============================] - 10s 989us/sample - loss: 0.0961 - acc: 0.9666 - rec: 0.9428 - prec: 0.9554 - f1: 0.9460 - val_loss: 1.6103 - val_acc: 0.7262 - val_rec: 0.5437 - val_prec: 0.5850 - val_f1: 0.5545
Epoch 00018: early stopping

2648/2648 [==============================] - 0s 55us/sample - loss: 1.6103 - acc: 0.7262 - rec: 0.5573 - prec: 0.5903 - f1: 0.5608

SCORES:
[1.6102692403822148, 0.72620845, 0.5572695, 0.590308, 0.56076545]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='CNN_model', num_epochs=50, num_filters=64, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 72us/sample - loss: 0.5288 - acc: 0.7704 - rec: 0.6181 - prec: 0.6628 - f1: 0.6303
[0.5288368115072164, 0.7703928, 0.61809844, 0.66278565, 0.63028526]

Scores on test:
860/860 [==============================] - 0s 52us/sample - loss: 0.5145 - acc: 0.7674 - rec: 0.5582 - prec: 0.5790 - f1: 0.5582
[0.5144938449526942, 0.76744187, 0.55822426, 0.5790057, 0.5581704]

```


- BiLSTM_CNN_model
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0762 - acc: 0.9706 - rec: 0.9488 - prec: 0.9629 - f1: 0.9535
Epoch 00019: val_f1 did not improve from 0.65768

10592/10592 [==============================] - 66s 6ms/sample - loss: 0.0760 - acc: 0.9707 - rec: 0.9490 - prec: 0.9630 - f1: 0.9537 - val_loss: 1.1745 - val_acc: 0.7330 - val_rec: 0.6339 - val_prec: 0.5834 - val_f1: 0.5971
Epoch 00019: early stopping

2648/2648 [==============================] - 2s 902us/sample - loss: 1.1745 - acc: 0.7330 - rec: 0.6388 - prec: 0.5922 - f1: 0.6037

SCORES:
[1.1744722118910706, 0.73300606, 0.6388139, 0.59224755, 0.60367644]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM_CNN_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 1ms/sample - loss: 0.4822 - acc: 0.7889 - rec: 0.6355 - prec: 0.6991 - f1: 0.6558
[0.48223463092505753, 0.7888973, 0.6354634, 0.6990714, 0.6557676]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4328 - acc: 0.8233 - rec: 0.6417 - prec: 0.6821 - f1: 0.6461
[0.43281403502752613, 0.82325584, 0.6416741, 0.68206185, 0.6461425]

```


- BiLSTM2_CNN_model
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0633 - acc: 0.9747 - rec: 0.9591 - prec: 0.9638 - f1: 0.9593
Epoch 00022: val_f1 did not improve from 0.64637

10592/10592 [==============================] - 104s 10ms/sample - loss: 0.0632 - acc: 0.9748 - rec: 0.9592 - prec: 0.9639 - f1: 0.9595 - val_loss: 1.2933 - val_acc: 0.7545 - val_rec: 0.5506 - val_prec: 0.6563 - val_f1: 0.5866
Epoch 00022: early stopping

2648/2648 [==============================] - 4s 2ms/sample - loss: 1.2933 - acc: 0.7545 - rec: 0.5365 - prec: 0.6530 - f1: 0.5772

SCORES:
[1.29328932430809, 0.75453174, 0.5364641, 0.65301144, 0.5772064]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 8s 3ms/sample - loss: 0.5739 - acc: 0.7636 - rec: 0.6847 - prec: 0.6284 - f1: 0.6439
[0.5738602907275866, 0.76359516, 0.68468463, 0.62843716, 0.6438824]

Scores on test:
860/860 [==============================] - 2s 2ms/sample - loss: 0.4843 - acc: 0.7849 - rec: 0.7196 - prec: 0.5901 - f1: 0.6357
[0.48427356689475304, 0.78488374, 0.71958536, 0.5901449, 0.63571]

```

- BiLSTM2_CNN3_model
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0661 - acc: 0.9750 - rec: 0.9552 - prec: 0.9692 - f1: 0.9597
Epoch 00020: val_f1 did not improve from 0.65814

10592/10592 [==============================] - 63s 6ms/sample - loss: 0.0660 - acc: 0.9751 - rec: 0.9553 - prec: 0.9693 - f1: 0.9598 - val_loss: 1.0850 - val_acc: 0.7462 - val_rec: 0.5874 - val_prec: 0.6273 - val_f1: 0.5975
Epoch 00020: early stopping

2592/2648 [============================>.] - ETA: 0s - loss: 1.0879 - acc: 0.7458 - rec: 0.5839 - prec: 0.6223 - f1: 0.5922
2648/2648 [==============================] - 2s 935us/sample - loss: 1.0850 - acc: 0.7462 - rec: 0.5832 - prec: 0.6214 - f1: 0.5917

SCORES:
[1.0850487756585065, 0.74622357, 0.5832009, 0.6214002, 0.5916651]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2624/2648 [============================>.] - ETA: 0s - loss: 0.5142 - acc: 0.7748 - rec: 0.6796 - prec: 0.6550 - f1: 0.6582
2648/2648 [==============================] - 5s 2ms/sample - loss: 0.5116 - acc: 0.7761 - rec: 0.6835 - prec: 0.6562 - f1: 0.6606
[0.5115537531336268, 0.7760574, 0.68348515, 0.6561736, 0.6606434]

Scores on test:
832/860 [============================>.] - ETA: 0s - loss: 0.4316 - acc: 0.8065 - rec: 0.6323 - prec: 0.6427 - f1: 0.6282
860/860 [==============================] - 1s 2ms/sample - loss: 0.4250 - acc: 0.8070 - rec: 0.6367 - prec: 0.6436 - f1: 0.6311
[0.4250453504712083, 0.80697674, 0.6366677, 0.64359885, 0.63111985]


```

- BiLSTM2_CNN3_short_model
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.1388 - acc: 0.9455 - rec: 0.9135 - prec: 0.9206 - f1: 0.9134
Epoch 00018: val_f1 did not improve from 0.65417

10592/10592 [==============================] - 64s 6ms/sample - loss: 0.1387 - acc: 0.9456 - rec: 0.9138 - prec: 0.9204 - f1: 0.9135 - val_loss: 1.0582 - val_acc: 0.7406 - val_rec: 0.6222 - val_prec: 0.6041 - val_f1: 0.6047
Epoch 00018: early stopping

2648/2648 [==============================] - 2s 921us/sample - loss: 1.0582 - acc: 0.7406 - rec: 0.6221 - prec: 0.6045 - f1: 0.6031

SCORES:
[1.0581714021115145, 0.7405589, 0.62206864, 0.60451156, 0.6030551]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_short_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 2ms/sample - loss: 0.4786 - acc: 0.7900 - rec: 0.6327 - prec: 0.7019 - f1: 0.6541
[0.47863985584581725, 0.79003024, 0.63271105, 0.7019291, 0.6540549]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4248 - acc: 0.8302 - rec: 0.5047 - prec: 0.7900 - f1: 0.5948
[0.4248453781355259, 0.83023256, 0.5047276, 0.7900193, 0.5948329]

```

- BiLSTM2_CNN3_supershort_model
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0428 - acc: 0.9848 - rec: 0.9745 - prec: 0.9804 - f1: 0.9764
Epoch 00017: val_f1 did not improve from 0.65606

10592/10592 [==============================] - 108s 10ms/sample - loss: 0.0427 - acc: 0.9849 - rec: 0.9746 - prec: 0.9804 - f1: 0.9765 - val_loss: 1.4964 - val_acc: 0.7436 - val_rec: 0.5870 - val_prec: 0.6190 - val_f1: 0.5913
Epoch 00017: early stopping

2648/2648 [==============================] - 6s 2ms/sample - loss: 1.4964 - acc: 0.7436 - rec: 0.5827 - prec: 0.6164 - f1: 0.5893

SCORES:
[1.4963736289217393, 0.74358004, 0.5827098, 0.616443, 0.5892503]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_supershort_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 9s 3ms/sample - loss: 0.4600 - acc: 0.7953 - rec: 0.6003 - prec: 0.7337 - f1: 0.6491
[0.4599583976848608, 0.79531723, 0.60029477, 0.733659, 0.6490783]

Scores on test:
860/860 [==============================] - 2s 2ms/sample - loss: 0.4178 - acc: 0.8349 - rec: 0.4979 - prec: 0.8273 - f1: 0.6111
[0.4178140885608141, 0.83488375, 0.4978712, 0.8273369, 0.6111303]

```


--- 

**Gotovi jednom svi modeli sa slicnim parametrima**

#################################################


- BiLSTM2_CNN3_short_model, epochs 5, filters 64
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.3737 - acc: 0.8374 - rec: 0.7316 - prec: 0.7738 - f1: 0.7387
10560/10592 [============================>.] - ETA: 0s - loss: 0.3736 - acc: 0.8375 - rec: 0.7321 - prec: 0.7737 - f1: 0.7389
Epoch 00005: val_f1 improved from 0.63851 to 0.65145, saving model to models/modelKeras_type=BiLSTM2_CNN3_short_model_proc=remove_stopwords_and_punctuation_textblob_epochs=5_emb_dim=300_vocab=7500

10592/10592 [==============================] - 83s 8ms/sample - loss: 0.3741 - acc: 0.8373 - rec: 0.7315 - prec: 0.7736 - f1: 0.7386 - val_loss: 0.4833 - val_acc: 0.7783 - val_rec: 0.6699 - val_prec: 0.6578 - val_f1: 0.6515

2648/2648 [==============================] - 3s 1ms/sample - loss: 0.4833 - acc: 0.7783 - rec: 0.6738 - prec: 0.6638 - f1: 0.6590

SCORES:
[0.4832660208746026, 0.77832323, 0.6737619, 0.66379476, 0.6589995]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=64, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_short_model', num_epochs=5, num_filters=64, oov_tok='<OOV>', pad_type='post', preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 6s 2ms/sample - loss: 0.4833 - acc: 0.7783 - rec: 0.6738 - prec: 0.6638 - f1: 0.6590
[0.4832660208746026, 0.77832323, 0.6737619, 0.66379476, 0.6589995]

Scores on test:
860/860 [==============================] - 2s 2ms/sample - loss: 0.4283 - acc: 0.8163 - rec: 0.6660 - prec: 0.6738 - f1: 0.6567
[0.4283393237479897, 0.81627905, 0.66597176, 0.6737802, 0.65668]
```

- BiLSTM2 + CNN3 short, epochs 50, filters 64
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.0810 - acc: 0.9696 - rec: 0.9498 - prec: 0.9589 - f1: 0.9521
10560/10592 [============================>.] - ETA: 0s - loss: 0.0811 - acc: 0.9695 - rec: 0.9494 - prec: 0.9590 - f1: 0.9519
Epoch 00022: val_f1 did not improve from 0.64409

10592/10592 [==============================] - 162s 15ms/sample - loss: 0.0812 - acc: 0.9694 - rec: 0.9491 - prec: 0.9592 - f1: 0.9518 - val_loss: 1.3563 - val_acc: 0.7432 - val_rec: 0.6028 - val_prec: 0.6131 - val_f1: 0.5996
Epoch 00022: early stopping

2648/2648 [==============================] - 7s 3ms/sample - loss: 1.3563 - acc: 0.7432 - rec: 0.5976 - prec: 0.6121 - f1: 0.5957

SCORES:
[1.356259297028049, 0.7432024, 0.59757155, 0.61209637, 0.59565383]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=64, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_short_model', num_epochs=50, num_filters=64, oov_tok='<OOV>', pad_type='post', preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 11s 4ms/sample - loss: 0.5067 - acc: 0.7772 - rec: 0.6888 - prec: 0.6570 - f1: 0.6628
[0.5066992101622492, 0.7771903, 0.68882906, 0.6570102, 0.6628343]

Scores on test:
860/860 [==============================] - 3s 3ms/sample - loss: 0.4575 - acc: 0.7930 - rec: 0.6545 - prec: 0.6172 - f1: 0.6226
[0.4575323815955672, 0.7930232, 0.6545476, 0.6172493, 0.6225591]
```


- BiLSTM2 + CNN3 short, epochs 50, filters 32, LSTM 32
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.1019 - acc: 0.9624 - rec: 0.9385 - prec: 0.9485 - f1: 0.9407
Epoch 00021: val_f1 did not improve from 0.65580

10592/10592 [==============================] - 119s 11ms/sample - loss: 0.1017 - acc: 0.9624 - rec: 0.9385 - prec: 0.9486 - f1: 0.9408 - val_loss: 1.1596 - val_acc: 0.7500 - val_rec: 0.6322 - val_prec: 0.6167 - val_f1: 0.6127
Epoch 00021: early stopping

2648/2648 [==============================] - 6s 2ms/sample - loss: 1.1596 - acc: 0.7500 - rec: 0.6332 - prec: 0.6247 - f1: 0.6174

SCORES:
[1.159556385163454, 0.75, 0.6331867, 0.62465006, 0.617377]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_short_model', num_epochs=50, num_filters=32, oov_tok='<OOV>', pad_type='post', preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 11s 4ms/sample - loss: 0.4712 - acc: 0.7931 - rec: 0.6253 - prec: 0.7219 - f1: 0.6595
[0.47117471159224783, 0.79305136, 0.62532, 0.7218655, 0.6594976]

Scores on test:
860/860 [==============================] - 3s 3ms/sample - loss: 0.4281 - acc: 0.8337 - rec: 0.4976 - prec: 0.8268 - f1: 0.6032
[0.42813846863979516, 0.8337209, 0.49763694, 0.82676363, 0.60322064]

```

- BiLSTM2 + CNN3 short, epochs 50, filters 16
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.1043 - acc: 0.9592 - rec: 0.9342 - prec: 0.9425 - f1: 0.9355
Epoch 00020: val_f1 did not improve from 0.65929

10592/10592 [==============================] - 97s 9ms/sample - loss: 0.1041 - acc: 0.9593 - rec: 0.9344 - prec: 0.9427 - f1: 0.9357 - val_loss: 1.1658 - val_acc: 0.7372 - val_rec: 0.5993 - val_prec: 0.6008 - val_f1: 0.5886
Epoch 00020: early stopping

2648/2648 [==============================] - 5s 2ms/sample - loss: 1.1658 - acc: 0.7372 - rec: 0.6012 - prec: 0.5982 - f1: 0.5903

SCORES:
[1.1658438424329383, 0.73716015, 0.601184, 0.59816664, 0.5902766]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=64, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_short_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 6s 2ms/sample - loss: 0.5067 - acc: 0.7772 - rec: 0.6888 - prec: 0.6570 - f1: 0.6628
[0.5066992101622492, 0.7771903, 0.68882906, 0.6570102, 0.6628343]

Scores on test:
860/860 [==============================] - 2s 2ms/sample - loss: 0.4575 - acc: 0.7930 - rec: 0.6545 - prec: 0.6172 - f1: 0.6226
[0.4575323815955672, 0.7930232, 0.6545476, 0.6172493, 0.6225591]

```

- BiLSTM2 + CNN3 short, filters 16, LR 0.0001
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.3588 - acc: 0.8467 - rec: 0.7342 - prec: 0.7894 - f1: 0.7504
Epoch 00030: val_f1 did not improve from 0.65957

10592/10592 [==============================] - 171s 16ms/sample - loss: 0.3585 - acc: 0.8469 - rec: 0.7344 - prec: 0.7897 - f1: 0.7507 - val_loss: 0.5215 - val_acc: 0.7753 - val_rec: 0.6620 - val_prec: 0.6607 - val_f1: 0.6499
Epoch 00030: early stopping

2648/2648 [==============================] - 10s 4ms/sample - loss: 0.5215 - acc: 0.7753 - rec: 0.6644 - prec: 0.6578 - f1: 0.6511

SCORES:
[0.5215204945593802, 0.7753021, 0.6643734, 0.65784395, 0.6511318]

Arguments:
----------
Namespace(LR=0.0001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=64, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_short_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 11s 4ms/sample - loss: 0.4712 - acc: 0.7931 - rec: 0.6253 - prec: 0.7219 - f1: 0.6595
[0.47117471159224783, 0.79305136, 0.62532, 0.7218655, 0.6594976]

Scores on test:
860/860 [==============================] - 3s 4ms/sample - loss: 0.4281 - acc: 0.8337 - rec: 0.4976 - prec: 0.8268 - f1: 0.6032
[0.42813846863979516, 0.8337209, 0.49763694, 0.82676363, 0.60322064]

```

- BiLSTM2 CNN3 supershort, filters 16, lstm out 32
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0448 - acc: 0.9852 - rec: 0.9742 - prec: 0.9821 - f1: 0.9770
Epoch 00017: val_f1 did not improve from 0.64698

10592/10592 [==============================] - 55s 5ms/sample - loss: 0.0447 - acc: 0.9853 - rec: 0.9743 - prec: 0.9821 - f1: 0.9770 - val_loss: 1.5422 - val_acc: 0.7364 - val_rec: 0.6231 - val_prec: 0.6000 - val_f1: 0.6002
Epoch 00017: early stopping

2648/2648 [==============================] - 2s 800us/sample - loss: 1.5422 - acc: 0.7364 - rec: 0.6199 - prec: 0.5954 - f1: 0.5981

SCORES:
[1.5422082051769845, 0.73640484, 0.6199382, 0.59538984, 0.5980996]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_supershort_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 2ms/sample - loss: 0.4631 - acc: 0.7927 - rec: 0.6026 - prec: 0.7211 - f1: 0.6468
[0.46309578760873155, 0.7926737, 0.6025862, 0.7210845, 0.6467714]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4137 - acc: 0.8395 - rec: 0.5011 - prec: 0.8437 - f1: 0.6106
[0.4137064877637597, 0.8395349, 0.50113755, 0.843739, 0.6105873]


```

- BiLSTM2 CNN3 model, lstm out = 32, 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.0786 - acc: 0.9703 - rec: 0.9497 - prec: 0.9616 - f1: 0.9533
Epoch 00017: val_f1 did not improve from 0.66581

10592/10592 [==============================] - 75s 7ms/sample - loss: 0.0789 - acc: 0.9703 - rec: 0.9499 - prec: 0.9614 - f1: 0.9533 - val_loss: 1.2629 - val_acc: 0.7553 - val_rec: 0.5747 - val_prec: 0.6594 - val_f1: 0.5995
Epoch 00017: early stopping

2648/2648 [==============================] - 3s 1ms/sample - loss: 1.2629 - acc: 0.7553 - rec: 0.5658 - prec: 0.6482 - f1: 0.5943

SCORES:
[1.2628837548353882, 0.755287, 0.56576526, 0.6481515, 0.59425765]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 2ms/sample - loss: 0.4630 - acc: 0.7851 - rec: 0.6778 - prec: 0.6787 - f1: 0.6676
[0.4630266522532864, 0.78512084, 0.67782676, 0.6787368, 0.6675677]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4118 - acc: 0.8256 - rec: 0.5510 - prec: 0.7419 - f1: 0.6144
[0.41183450520038606, 0.8255814, 0.5510119, 0.74187905, 0.6144029]


```


## Preprocessing - TwitterTokenizer (sanja)

- BiLSTM2_CNN3_short_model
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.1188 - acc: 0.9547 - rec: 0.9271 - prec: 0.9369 - f1: 0.9287
Epoch 00021: val_f1 did not improve from 0.65011

10592/10592 [==============================] - 61s 6ms/sample - loss: 0.1185 - acc: 0.9549 - rec: 0.9274 - prec: 0.9371 - f1: 0.9289 - val_loss: 1.0674 - val_acc: 0.7474 - val_rec: 0.6168 - val_prec: 0.6181 - val_f1: 0.6044
Epoch 00021: early stopping

2648/2648 [==============================] - 2s 917us/sample - loss: 1.0674 - acc: 0.7474 - rec: 0.6140 - prec: 0.6159 - f1: 0.6045

SCORES:
[1.0673633788647607, 0.7473565, 0.61399794, 0.6158508, 0.6045157]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_short_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 2ms/sample - loss: 0.5268 - acc: 0.7734 - rec: 0.6720 - prec: 0.6513 - f1: 0.6520
[0.5267848439537146, 0.7734139, 0.6719924, 0.65129554, 0.65204674]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4732 - acc: 0.8174 - rec: 0.5953 - prec: 0.6949 - f1: 0.6322
[0.4732070698294529, 0.8174419, 0.5953094, 0.6948628, 0.63219887]
```

## Preprocessing - no preprocessing

- BiLSTM2_CNN3_short_model

```
10560/10592 [============================>.] - ETA: 0s - loss: 0.2833 - acc: 0.8873 - rec: 0.8226 - prec: 0.8347 - f1: 0.8209
Epoch 00009: val_f1 did not improve from 0.67748

10592/10592 [==============================] - 61s 6ms/sample - loss: 0.2831 - acc: 0.8873 - rec: 0.8228 - prec: 0.8344 - f1: 0.8208 - val_loss: 0.5791 - val_acc: 0.7666 - val_rec: 0.6567 - val_prec: 0.6514 - val_f1: 0.6420
Epoch 00009: early stopping

2648/2648 [==============================] - 2s 875us/sample - loss: 0.5791 - acc: 0.7666 - rec: 0.6488 - prec: 0.6402 - f1: 0.6363

SCORES:
[0.5790688983443281, 0.7666163, 0.6488238, 0.64021593, 0.63626784]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras', model_type='BiLSTM2_CNN3_short_model', num_epochs=50, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='no_preprocessing', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 2ms/sample - loss: 0.4687 - acc: 0.7813 - rec: 0.7012 - prec: 0.6592 - f1: 0.6703
[0.4686959538034802, 0.7813444, 0.70122886, 0.6592447, 0.6703403]

Scores on test:
860/860 [==============================] - 1s 2ms/sample - loss: 0.4243 - acc: 0.8070 - rec: 0.6581 - prec: 0.6365 - f1: 0.6368
[0.4242650256600491, 0.80697674, 0.65812385, 0.6365452, 0.6367698]

```


------------------------------

## RUn 2 i 3

**Basic no emb**
- 1: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1942 - acc: 0.9274 - rec: 0.8602 - prec: 0.9169 - f1: 0.8800
Epoch 00008: val_f1 did not improve from 0.59769

10592/10592 [==============================] - 11s 1ms/sample - loss: 0.1940 - acc: 0.9275 - rec: 0.8599 - prec: 0.9174 - f1: 0.8801 - val_loss: 0.8617 - val_acc: 0.7492 - val_rec: 0.5321 - val_prec: 0.6465 - val_f1: 0.5698
Epoch 00008: early stopping

2648/2648 [==============================] - 0s 54us/sample - loss: 0.8617 - acc: 0.7492 - rec: 0.5253 - prec: 0.6361 - f1: 0.5654

SCORES:
[0.8616731038986736, 0.7492447, 0.5252508, 0.6361413, 0.5654126]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras1', model_type='basic_no_emb_model', num_epochs=10, num_filters=64, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 67us/sample - loss: 0.5534 - acc: 0.7625 - rec: 0.5616 - prec: 0.6653 - f1: 0.5987
[0.5534110775166768, 0.76246226, 0.5615798, 0.66527784, 0.5987098]

Scores on test:
860/860 [==============================] - 0s 53us/sample - loss: 0.5356 - acc: 0.7709 - rec: 0.4581 - prec: 0.6179 - f1: 0.5155
[0.5355715511843215, 0.77093023, 0.45807776, 0.61787313, 0.51550984]

```
- 2: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1735 - acc: 0.9344 - rec: 0.8757 - prec: 0.9261 - f1: 0.8937
Epoch 00010: val_f1 did not improve from 0.58960

10592/10592 [==============================] - 11s 1ms/sample - loss: 0.1735 - acc: 0.9345 - rec: 0.8761 - prec: 0.9261 - f1: 0.8938 - val_loss: 0.9308 - val_acc: 0.7262 - val_rec: 0.5870 - val_prec: 0.5927 - val_f1: 0.5752

2648/2648 [==============================] - 0s 53us/sample - loss: 0.9308 - acc: 0.7262 - rec: 0.5794 - prec: 0.5829 - f1: 0.5707

SCORES:
[0.9307756674253689, 0.72620845, 0.579372, 0.58291095, 0.5707242]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2', model_type='basic_no_emb_model', num_epochs=10, num_filters=64, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 69us/sample - loss: 0.7994 - acc: 0.7481 - rec: 0.5623 - prec: 0.6292 - f1: 0.5829
[0.7993530695892173, 0.7481118, 0.56233066, 0.62918156, 0.5828674]

Scores on test:
860/860 [==============================] - 0s 50us/sample - loss: 1.0503 - acc: 0.7012 - rec: 0.5090 - prec: 0.4862 - f1: 0.4838
[1.0502550669880801, 0.7011628, 0.5090117, 0.48617852, 0.48383796]

```

- 3: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1587 - acc: 0.9442 - rec: 0.9026 - prec: 0.9288 - f1: 0.9103
Epoch 00010: val_f1 did not improve from 0.58805

10592/10592 [==============================] - 10s 957us/sample - loss: 0.1589 - acc: 0.9441 - rec: 0.9024 - prec: 0.9287 - f1: 0.9102 - val_loss: 1.0348 - val_acc: 0.7085 - val_rec: 0.6180 - val_prec: 0.5589 - val_f1: 0.5744

2648/2648 [==============================] - 0s 52us/sample - loss: 1.0348 - acc: 0.7085 - rec: 0.6077 - prec: 0.5505 - f1: 0.5670

SCORES:
[1.034759555878596, 0.7084592, 0.6077107, 0.5505128, 0.56697017]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3', model_type='basic_no_emb_model', num_epochs=10, num_filters=64, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 73us/sample - loss: 0.8075 - acc: 0.7281 - rec: 0.6018 - prec: 0.5811 - f1: 0.5808
[0.8074768480937646, 0.72809666, 0.601778, 0.5810636, 0.58082837]

Scores on test:
860/860 [==============================] - 0s 52us/sample - loss: 1.0465 - acc: 0.6965 - rec: 0.5686 - prec: 0.4836 - f1: 0.5064
[1.046521896123886, 0.6965116, 0.5686219, 0.4835665, 0.50639355]

```


**Basic**
- 2
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.1836 - acc: 0.9326 - rec: 0.8764 - prec: 0.9220 - f1: 0.8924
Epoch 00009: val_f1 did not improve from 0.60871

10592/10592 [==============================] - 11s 1ms/sample - loss: 0.1836 - acc: 0.9325 - rec: 0.8765 - prec: 0.9217 - f1: 0.8923 - val_loss: 0.8738 - val_acc: 0.7270 - val_rec: 0.6008 - val_prec: 0.5853 - val_f1: 0.5798
Epoch 00009: early stopping

2648/2648 [==============================] - 0s 51us/sample - loss: 0.8738 - acc: 0.7270 - rec: 0.6011 - prec: 0.5780 - f1: 0.5793

SCORES:
[0.8738254043991112, 0.72696376, 0.6010546, 0.57796043, 0.57932544]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2', model_type='basic_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 76us/sample - loss: 0.5592 - acc: 0.7700 - rec: 0.5661 - prec: 0.6741 - f1: 0.6058
[0.5591787370850312, 0.7700151, 0.56611043, 0.6740835, 0.6057811]

Scores on test:
860/860 [==============================] - 0s 51us/sample - loss: 0.5529 - acc: 0.7837 - rec: 0.4963 - prec: 0.6280 - f1: 0.5436
[0.5528563254101332, 0.7837209, 0.4963177, 0.6280181, 0.5436187]

```
- 3
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.1877 - acc: 0.9317 - rec: 0.8724 - prec: 0.9232 - f1: 0.8889
Epoch 00009: val_f1 did not improve from 0.61265

10592/10592 [==============================] - 17s 2ms/sample - loss: 0.1878 - acc: 0.9316 - rec: 0.8721 - prec: 0.9234 - f1: 0.8888 - val_loss: 0.9060 - val_acc: 0.7542 - val_rec: 0.5012 - val_prec: 0.6708 - val_f1: 0.5628
Epoch 00009: early stopping
2648/2648 [==============================] - 0s 134us/sample - loss: 0.9060 - acc: 0.7542 - rec: 0.4960 - prec: 0.6674 - f1: 0.5567

SCORES:
[0.9059868478342846, 0.7541541, 0.4959851, 0.6673695, 0.5567075]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3', model_type='basic_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 1s 199us/sample - loss: 0.5644 - acc: 0.7651 - rec: 0.5912 - prec: 0.6621 - f1: 0.6163
[0.5643898493573745, 0.7651057, 0.5912168, 0.66211426, 0.61629236]

Scores on test:
860/860 [==============================] - 0s 131us/sample - loss: 0.6348 - acc: 0.7326 - rec: 0.6015 - prec: 0.5237 - f1: 0.5473
[0.6348478479440822, 0.73255813, 0.60153574, 0.5236528, 0.54726434]

```

**BiLSTM model**
- 2
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.1601 - acc: 0.9362 - rec: 0.8934 - prec: 0.9161 - f1: 0.8996
Epoch 00009: val_f1 did not improve from 0.63165

10592/10592 [==============================] - 49s 5ms/sample - loss: 0.1606 - acc: 0.9359 - rec: 0.8930 - prec: 0.9154 - f1: 0.8990 - val_loss: 0.8655 - val_acc: 0.7466 - val_rec: 0.5924 - val_prec: 0.6267 - val_f1: 0.5978
Epoch 00009: early stopping

2648/2648 [==============================] - 1s 383us/sample - loss: 0.8655 - acc: 0.7466 - rec: 0.5877 - prec: 0.6176 - f1: 0.5917

SCORES:
[0.8655441464614292, 0.7466012, 0.58773994, 0.6176451, 0.59171605]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2', model_type='BiLSTM_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 1s 498us/sample - loss: 0.5331 - acc: 0.7829 - rec: 0.5872 - prec: 0.7062 - f1: 0.6310
[0.5331085545328809, 0.782855, 0.5871571, 0.7062019, 0.63103414]

Scores on test:
860/860 [==============================] - 0s 450us/sample - loss: 0.4671 - acc: 0.8302 - rec: 0.4812 - prec: 0.8046 - f1: 0.5871
[0.46711185761662416, 0.83023256, 0.4811751, 0.8045856, 0.5870791]

```

- 3: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.1676 - acc: 0.9328 - rec: 0.8869 - prec: 0.9084 - f1: 0.8931
Epoch 00009: val_f1 did not improve from 0.63370

10592/10592 [==============================] - 58s 5ms/sample - loss: 0.1680 - acc: 0.9325 - rec: 0.8867 - prec: 0.9083 - f1: 0.8929 - val_loss: 0.8812 - val_acc: 0.7557 - val_rec: 0.5600 - val_prec: 0.6545 - val_f1: 0.5911
Epoch 00009: early stopping

2648/2648 [==============================] - 2s 882us/sample - loss: 0.8812 - acc: 0.7557 - rec: 0.5628 - prec: 0.6595 - f1: 0.5932

SCORES:
[0.8812109296775656, 0.75566465, 0.56279284, 0.65948635, 0.59323984]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3', model_type='BiLSTM_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 1s 527us/sample - loss: 0.5397 - acc: 0.7840 - rec: 0.5851 - prec: 0.7127 - f1: 0.6311
[0.5396915298304169, 0.78398794, 0.5850823, 0.71268255, 0.63108295]

Scores on test:
860/860 [==============================] - 0s 452us/sample - loss: 0.4389 - acc: 0.8233 - rec: 0.5509 - prec: 0.7229 - f1: 0.6148
[0.4388537290484406, 0.82325584, 0.55087864, 0.7229117, 0.6147892]

```

**CNN 16**
- 1: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1983 - acc: 0.9264 - rec: 0.8671 - prec: 0.9112 - f1: 0.8816
Epoch 00008: val_f1 did not improve from 0.64149

10592/10592 [==============================] - 10s 974us/sample - loss: 0.1981 - acc: 0.9265 - rec: 0.8672 - prec: 0.9117 - f1: 0.8819 - val_loss: 0.9086 - val_acc: 0.7523 - val_rec: 0.4760 - val_prec: 0.6729 - val_f1: 0.5396
Epoch 00008: early stopping

2648/2648 [==============================] - 0s 52us/sample - loss: 0.9086 - acc: 0.7523 - rec: 0.4706 - prec: 0.6728 - f1: 0.5411

SCORES:
[0.9085766844158807, 0.7522659, 0.47056377, 0.6727813, 0.5410964]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras1_cnn16', model_type='CNN_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 68us/sample - loss: 0.5379 - acc: 0.7617 - rec: 0.6646 - prec: 0.6342 - f1: 0.6388
[0.5378660439904723, 0.76170695, 0.6645518, 0.63420916, 0.638796]

Scores on test:
860/860 [==============================] - 0s 52us/sample - loss: 0.6437 - acc: 0.7000 - rec: 0.7175 - prec: 0.4777 - f1: 0.5635
[0.6437306745107784, 0.7, 0.7174567, 0.47766522, 0.56350887]

```

- 2: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.2214 - acc: 0.9138 - rec: 0.8353 - prec: 0.8999 - f1: 0.8582
Epoch 00007: val_f1 did not improve from 0.63901

10592/10592 [==============================] - 17s 2ms/sample - loss: 0.2215 - acc: 0.9139 - rec: 0.8355 - prec: 0.8999 - f1: 0.8583 - val_loss: 0.7610 - val_acc: 0.7504 - val_rec: 0.5760 - val_prec: 0.6392 - val_f1: 0.5941
Epoch 00007: early stopping

2648/2648 [==============================] - 0s 115us/sample - loss: 0.7610 - acc: 0.7504 - rec: 0.5709 - prec: 0.6283 - f1: 0.5892

SCORES:
[0.7609558352170754, 0.75037766, 0.57090867, 0.6282555, 0.5892085]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2_cnn16', model_type='CNN_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 168us/sample - loss: 0.5215 - acc: 0.7745 - rec: 0.6377 - prec: 0.6672 - f1: 0.6412
[0.5214502970797777, 0.7745468, 0.6376867, 0.66721237, 0.64120764]

Scores on test:
860/860 [==============================] - 0s 135us/sample - loss: 0.4715 - acc: 0.7988 - rec: 0.5724 - prec: 0.6538 - f1: 0.5977
[0.4715170063251673, 0.7988372, 0.5724, 0.6537677, 0.5977012]

```

- 3: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1813 - acc: 0.9334 - rec: 0.8775 - prec: 0.9220 - f1: 0.8928
Epoch 00009: val_f1 did not improve from 0.62241

10592/10592 [==============================] - 10s 964us/sample - loss: 0.1817 - acc: 0.9331 - rec: 0.8764 - prec: 0.9224 - f1: 0.8924 - val_loss: 0.9143 - val_acc: 0.7534 - val_rec: 0.5176 - val_prec: 0.6597 - val_f1: 0.5677
Epoch 00009: early stopping

2648/2648 [==============================] - 0s 53us/sample - loss: 0.9143 - acc: 0.7534 - rec: 0.5169 - prec: 0.6519 - f1: 0.5672

SCORES:
[0.9142572598875109, 0.7533988, 0.51692414, 0.65191674, 0.567231]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3_cnn16', model_type='CNN_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 74us/sample - loss: 0.5677 - acc: 0.7685 - rec: 0.6172 - prec: 0.6605 - f1: 0.6276
[0.5676792866333734, 0.76850456, 0.61716914, 0.6604952, 0.6276202]

Scores on test:
860/860 [==============================] - 0s 51us/sample - loss: 0.6567 - acc: 0.7256 - rec: 0.6199 - prec: 0.5042 - f1: 0.5452
[0.6567106496456058, 0.7255814, 0.6198835, 0.5042244, 0.5451991]

```

**CNN 64**
- 1: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1822 - acc: 0.9331 - rec: 0.8764 - prec: 0.9220 - f1: 0.8922
Epoch 00009: val_f1 did not improve from 0.62176

10592/10592 [==============================] - 10s 979us/sample - loss: 0.1822 - acc: 0.9333 - rec: 0.8764 - prec: 0.9225 - f1: 0.8924 - val_loss: 0.9067 - val_acc: 0.7564 - val_rec: 0.5400 - val_prec: 0.6646 - val_f1: 0.5806
Epoch 00009: early stopping

2648/2648 [==============================] - 0s 52us/sample - loss: 0.9067 - acc: 0.7564 - rec: 0.5325 - prec: 0.6528 - f1: 0.5774

SCORES:
[0.9066743117804974, 0.75641996, 0.5324592, 0.65282595, 0.57741576]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras1_cnn64', model_type='CNN_model', num_epochs=10, num_filters=64, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 66us/sample - loss: 0.5645 - acc: 0.7685 - rec: 0.6140 - prec: 0.6615 - f1: 0.6273
[0.5644911036930775, 0.76850456, 0.6140077, 0.6614915, 0.62725025]

Scores on test:

860/860 [==============================] - 0s 52us/sample - loss: 0.6307 - acc: 0.7349 - rec: 0.5835 - prec: 0.5232 - f1: 0.5382
[0.6307148420533468, 0.7348837, 0.5834647, 0.5231662, 0.53820294]

```

- 2: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1890 - acc: 0.9272 - rec: 0.8601 - prec: 0.9200 - f1: 0.8818
Epoch 00009: val_f1 did not improve from 0.61858

10592/10592 [==============================] - 10s 957us/sample - loss: 0.1891 - acc: 0.9270 - rec: 0.8593 - prec: 0.9203 - f1: 0.8815 - val_loss: 0.8584 - val_acc: 0.7474 - val_rec: 0.5860 - val_prec: 0.6344 - val_f1: 0.5910
Epoch 00009: early stopping

2648/2648 [==============================] - 0s 52us/sample - loss: 0.8584 - acc: 0.7474 - rec: 0.5838 - prec: 0.6222 - f1: 0.5918

SCORES:
[0.8583884968498322, 0.7473565, 0.5837786, 0.622225, 0.5918244]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2_cnn64', model_type='CNN_model', num_epochs=10, num_filters=64, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 68us/sample - loss: 0.6039 - acc: 0.7364 - rec: 0.6712 - prec: 0.5903 - f1: 0.6167
[0.6038672938447704, 0.73640484, 0.67119634, 0.59025466, 0.6166906]

Scores on test:
860/860 [==============================] - 0s 50us/sample - loss: 0.7448 - acc: 0.6907 - rec: 0.7307 - prec: 0.4743 - f1: 0.5602
[0.7448452856651572, 0.69069767, 0.7307442, 0.4742784, 0.5601777]

```

- 3: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.2004 - acc: 0.9236 - rec: 0.8537 - prec: 0.9128 - f1: 0.8751
Epoch 00008: val_f1 did not improve from 0.63514

10592/10592 [==============================] - 10s 988us/sample - loss: 0.2006 - acc: 0.9235 - rec: 0.8534 - prec: 0.9126 - f1: 0.8748 - val_loss: 0.8187 - val_acc: 0.7515 - val_rec: 0.5377 - val_prec: 0.6475 - val_f1: 0.5780
Epoch 00008: early stopping

2648/2648 [==============================] - 0s 67us/sample - loss: 0.8187 - acc: 0.7515 - rec: 0.5304 - prec: 0.6439 - f1: 0.5713

SCORES:
[0.8186879655025516, 0.75151056, 0.53039706, 0.6438549, 0.5713293]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3_cnn64', model_type='CNN_model', num_epochs=10, num_filters=64, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 68us/sample - loss: 0.5240 - acc: 0.7723 - rec: 0.6070 - prec: 0.6704 - f1: 0.6276
[0.5239867657152908, 0.772281, 0.60704, 0.670398, 0.6276357]

Scores on test:
860/860 [==============================] - 0s 53us/sample - loss: 0.5333 - acc: 0.7523 - rec: 0.5597 - prec: 0.5601 - f1: 0.5451
[0.5333057104155075, 0.7523256, 0.5597377, 0.56010914, 0.5451295]

```

**CNN 256**
- 1: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1840 - acc: 0.9306 - rec: 0.8664 - prec: 0.9212 - f1: 0.8854
Epoch 00009: val_f1 did not improve from 0.62650

10592/10592 [==============================] - 11s 1000us/sample - loss: 0.1835 - acc: 0.9308 - rec: 0.8667 - prec: 0.9216 - f1: 0.8859 - val_loss: 0.8831 - val_acc: 0.7232 - val_rec: 0.6252 - val_prec: 0.5702 - val_f1: 0.5828
Epoch 00009: early stopping
2648/2648 [==============================] - 0s 55us/sample - loss: 0.8831 - acc: 0.7232 - rec: 0.6185 - prec: 0.5723 - f1: 0.5838

SCORES:
[0.8831492214044415, 0.7231873, 0.61853915, 0.5723056, 0.5838038]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras1_cnn256', model_type='CNN_model', num_epochs=10, num_filters=256, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 70us/sample - loss: 0.5992 - acc: 0.7466 - rec: 0.6594 - prec: 0.6074 - f1: 0.6230
[0.5992351407550973, 0.7466012, 0.65940285, 0.6074342, 0.62296593]

Scores on test:
860/860 [==============================] - 0s 52us/sample - loss: 0.6468 - acc: 0.7326 - rec: 0.6296 - prec: 0.5210 - f1: 0.5583
[0.6467662929102432, 0.73255813, 0.6296144, 0.52104634, 0.5582805]

```

- 2: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.2032 - acc: 0.9214 - rec: 0.8564 - prec: 0.9026 - f1: 0.8705
Epoch 00008: val_f1 did not improve from 0.62818

10592/10592 [==============================] - 11s 1ms/sample - loss: 0.2036 - acc: 0.9214 - rec: 0.8559 - prec: 0.9029 - f1: 0.8704 - val_loss: 0.8501 - val_acc: 0.7606 - val_rec: 0.5186 - val_prec: 0.6797 - val_f1: 0.5770
Epoch 00008: early stopping

2648/2648 [==============================] - 0s 56us/sample - loss: 0.8501 - acc: 0.7606 - rec: 0.5185 - prec: 0.6685 - f1: 0.5732

SCORES:
[0.8500767324986415, 0.76057404, 0.51846004, 0.668522, 0.57315016]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2_cnn256', model_type='CNN_model', num_epochs=10, num_filters=256, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 66us/sample - loss: 0.5316 - acc: 0.7708 - rec: 0.6186 - prec: 0.6652 - f1: 0.6313
[0.5315574993719867, 0.7707704, 0.6185707, 0.665177, 0.6312708]

Scores on test:
860/860 [==============================] - 0s 52us/sample - loss: 0.5306 - acc: 0.7698 - rec: 0.5687 - prec: 0.5955 - f1: 0.5696
[0.5306140230145565, 0.76976746, 0.5686557, 0.5955217, 0.569589]

```

- 3: 
```
10528/10592 [============================>.] - ETA: 0s - loss: 0.1774 - acc: 0.9353 - rec: 0.8826 - prec: 0.9202 - f1: 0.8956
Epoch 00009: val_f1 did not improve from 0.62826

10592/10592 [==============================] - 11s 995us/sample - loss: 0.1779 - acc: 0.9351 - rec: 0.8826 - prec: 0.9195 - f1: 0.8954 - val_loss: 0.8904 - val_acc: 0.7202 - val_rec: 0.6260 - val_prec: 0.5655 - val_f1: 0.5834
Epoch 00009: early stopping

2648/2648 [==============================] - 0s 60us/sample - loss: 0.8904 - acc: 0.7202 - rec: 0.6231 - prec: 0.5679 - f1: 0.5837

SCORES:
[0.8903709900343166, 0.72016615, 0.623067, 0.5679489, 0.58368164]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3_cnn256', model_type='CNN_model', num_epochs=10, num_filters=256, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 0s 76us/sample - loss: 0.5978 - acc: 0.7432 - rec: 0.6823 - prec: 0.5998 - f1: 0.6283
[0.5978339390992398, 0.7432024, 0.68234605, 0.5997569, 0.6283056]

Scores on test:
860/860 [==============================] - 0s 51us/sample - loss: 0.5946 - acc: 0.7547 - rec: 0.6321 - prec: 0.5609 - f1: 0.5804
[0.5945663104916727, 0.7546512, 0.63214236, 0.56092775, 0.5803653]
```


**BiLSTM CNN model**

- 2: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.2189 - acc: 0.9122 - rec: 0.8584 - prec: 0.8741 - f1: 0.8591
Epoch 00008: val_f1 did not improve from 0.65506

10592/10592 [==============================] - 70s 7ms/sample - loss: 0.2191 - acc: 0.9122 - rec: 0.8583 - prec: 0.8742 - f1: 0.8591 - val_loss: 0.6360 - val_acc: 0.7602 - val_rec: 0.6290 - val_prec: 0.6488 - val_f1: 0.6276
Epoch 00008: early stopping

2648/2648 [==============================] - 3s 977us/sample - loss: 0.6360 - acc: 0.7602 - rec: 0.6269 - prec: 0.6378 - f1: 0.6224

SCORES:
[0.6359823987203063, 0.7601964, 0.62690043, 0.63776404, 0.6224118]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2', model_type='BiLSTM_CNN_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 3s 1ms/sample - loss: 0.4740 - acc: 0.7881 - rec: 0.6415 - prec: 0.6943 - f1: 0.6550
[0.47400585559739805, 0.78814197, 0.6414882, 0.69428205, 0.65502936]

Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4200 - acc: 0.8267 - rec: 0.5502 - prec: 0.7339 - f1: 0.6130
[0.41996017541996267, 0.8267442, 0.5501713, 0.73386246, 0.613036]

```

- 3: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.2168 - acc: 0.9117 - rec: 0.8661 - prec: 0.8703 - f1: 0.8609
Epoch 00008: val_f1 did not improve from 0.66232

10592/10592 [==============================] - 70s 7ms/sample - loss: 0.2170 - acc: 0.9115 - rec: 0.8662 - prec: 0.8698 - f1: 0.8607 - val_loss: 0.6604 - val_acc: 0.7583 - val_rec: 0.6131 - val_prec: 0.6457 - val_f1: 0.6192
Epoch 00008: early stopping

2648/2648 [==============================] - 3s 951us/sample - loss: 0.6604 - acc: 0.7583 - rec: 0.6088 - prec: 0.6461 - f1: 0.6140

SCORES:
[0.6603959763698347, 0.7583082, 0.6087597, 0.6460767, 0.6140414]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3', model_type='BiLSTM_CNN_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 3s 1ms/sample - loss: 0.4738 - acc: 0.7791 - rec: 0.6893 - prec: 0.6596 - f1: 0.6647
[0.47378812896881217, 0.77907854, 0.68927574, 0.6596058, 0.6646657]

Scores on test:
860/860 [==============================] - 1s 944us/sample - loss: 0.4440 - acc: 0.8140 - rec: 0.6451 - prec: 0.6656 - f1: 0.6418
[0.4439623890921127, 0.81395346, 0.64509857, 0.66562194, 0.6418397]

```

**BiLSTM2 CNN3**
- 2: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.2081 - acc: 0.9177 - rec: 0.8706 - prec: 0.8804 - f1: 0.8682
Epoch 00008: val_f1 did not improve from 0.67534

10592/10592 [==============================] - 117s 11ms/sample - loss: 0.2079 - acc: 0.9179 - rec: 0.8710 - prec: 0.8806 - f1: 0.8685 - val_loss: 0.6538 - val_acc: 0.7708 - val_rec: 0.6524 - val_prec: 0.6511 - val_f1: 0.6407
Epoch 00008: early stopping

2648/2648 [==============================] - 5s 2ms/sample - loss: 0.6538 - acc: 0.7708 - rec: 0.6578 - prec: 0.6525 - f1: 0.6471

SCORES:
[0.6538196526625365, 0.7707704, 0.65780216, 0.652484, 0.6471314]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2', model_type='BiLSTM2_CNN3_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 6s 2ms/sample - loss: 0.4683 - acc: 0.7855 - rec: 0.6924 - prec: 0.6698 - f1: 0.6711
[0.46833498735442264, 0.7854985, 0.6923805, 0.6697642, 0.6711001]

Scores on test:
860/860 [==============================] - 2s 2ms/sample - loss: 0.4157 - acc: 0.8395 - rec: 0.6402 - prec: 0.7460 - f1: 0.6778
[0.41568076769972956, 0.8395349, 0.6401795, 0.7460131, 0.6777801]

```

- 3: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.2065 - acc: 0.9172 - rec: 0.8674 - prec: 0.8833 - f1: 0.8689
Epoch 00008: val_f1 did not improve from 0.65006

10592/10592 [==============================] - 117s 11ms/sample - loss: 0.2061 - acc: 0.9175 - rec: 0.8678 - prec: 0.8836 - f1: 0.8693 - val_loss: 0.6638 - val_acc: 0.7719 - val_rec: 0.6197 - val_prec: 0.6671 - val_f1: 0.6311
Epoch 00008: early stopping

2648/2648 [==============================] - 4s 1ms/sample - loss: 0.6638 - acc: 0.7719 - rec: 0.6182 - prec: 0.6653 - f1: 0.6316

SCORES:
[0.6638426927011178, 0.77190334, 0.61817306, 0.66533697, 0.6315716]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3', model_type='BiLSTM2_CNN3_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 6s 2ms/sample - loss: 0.4726 - acc: 0.7764 - rec: 0.6623 - prec: 0.6603 - f1: 0.6519
[0.472612017951343, 0.776435, 0.6622757, 0.66026396, 0.65193844]

Scores on test:
860/860 [==============================] - 2s 2ms/sample - loss: 0.4370 - acc: 0.7988 - rec: 0.6339 - prec: 0.6306 - f1: 0.6239
[0.4370402976523998, 0.7988372, 0.6339443, 0.6305977, 0.6238962]

```



**BiLSTM2 CNN3 short**
- 2: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.2736 - acc: 0.8906 - rec: 0.8221 - prec: 0.8463 - f1: 0.8257
Epoch 00009: val_f1 did not improve from 0.65718

10592/10592 [==============================] - 74s 7ms/sample - loss: 0.2736 - acc: 0.8908 - rec: 0.8223 - prec: 0.8465 - f1: 0.8260 - val_loss: 0.6278 - val_acc: 0.7719 - val_rec: 0.6446 - val_prec: 0.6702 - val_f1: 0.6426
Epoch 00009: early stopping

2648/2648 [==============================] - 3s 967us/sample - loss: 0.6278 - acc: 0.7719 - rec: 0.6326 - prec: 0.6555 - f1: 0.6345

SCORES:
[0.6277928465352678, 0.77190334, 0.6325667, 0.65550715, 0.6345067]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras2', model_type='BiLSTM2_CNN3_short_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 4s 2ms/sample - loss: 0.4694 - acc: 0.7847 - rec: 0.6726 - prec: 0.6832 - f1: 0.6660
[0.46942756980027317, 0.7847432, 0.6726009, 0.6832064, 0.6660438]

Scores on test:
860/860 [==============================] - 1s 2ms/sample - loss: 0.4173 - acc: 0.8326 - rec: 0.5961 - prec: 0.7419 - f1: 0.6503
[0.41733100892499436, 0.83255816, 0.5961305, 0.7419206, 0.6502978]

```

- 3: 
```
10560/10592 [============================>.] - ETA: 0s - loss: 0.2946 - acc: 0.8737 - rec: 0.8052 - prec: 0.8145 - f1: 0.8005
Epoch 00008: val_f1 did not improve from 0.66579

10592/10592 [==============================] - 114s 11ms/sample - loss: 0.2951 - acc: 0.8733 - rec: 0.8053 - prec: 0.8139 - f1: 0.8002 - val_loss: 0.5603 - val_acc: 0.7779 - val_rec: 0.6201 - val_prec: 0.6798 - val_f1: 0.6390
Epoch 00008: early stopping

2648/2648 [==============================] - 5s 2ms/sample - loss: 0.5603 - acc: 0.7779 - rec: 0.6210 - prec: 0.6764 - f1: 0.6361

SCORES:
[0.5602872665194947, 0.77794564, 0.6209658, 0.6763951, 0.63612187]

Arguments:
----------
Namespace(LR=0.001, data_file='../../Dataset-OLID/OLIDv1.0/data_subtask_a.csv', dropout=0.5, emb_dim=300, emb_file='../../../0_embeddings/glove.6B/glove.6B.300d.txt', kernel_size=3, lstm_out=32, max_len=64, model_name='modelKeras3', model_type='BiLSTM2_CNN3_short_model', num_epochs=10, num_filters=16, oov_tok='<OOV>', pad_type='post', pool_size=2, preproc='remove_stopwords_and_punctuation_textblob', strides=1, test_file='../../Dataset-OLID/OLIDv1.0/test_data_subtask_a.csv', train_portion=0.8, trunc_type='post', verbose=1, vocab_size=7500)

Scores on val:
2648/2648 [==============================] - 9s 3ms/sample - loss: 0.4690 - acc: 0.7863 - rec: 0.6850 - prec: 0.6758 - f1: 0.6707
[0.4690481904230089, 0.78625375, 0.6850168, 0.675808, 0.67068595]

Scores on test:
860/860 [==============================] - 2s 2ms/sample - loss: 0.4222 - acc: 0.8326 - rec: 0.5520 - prec: 0.7547 - f1: 0.6222
[0.4222217744173006, 0.83255816, 0.55204105, 0.7546512, 0.6221856]

```


## Test preprocessing on BiLSTM2_CNN3_short

1. no_preprocessing
```
```
2. remove_stopwords and punctuation
```
```
3. remove stopwords and punctuation textblob
```
Scores on test:
860/860 [==============================] - 1s 1ms/sample - loss: 0.4251 - acc: 0.8349 - rec: 0.5495 - prec: 0.7594 - f1: 0.6253
[0.42508711149526196, 0.83488375, 0.5495007, 0.75937015, 0.6252544]

Scores on no proc test:
860/860 [==============================] - 1s 946us/sample - loss: 0.4141 - acc: 0.8349 - rec: 0.5731 - prec: 0.7403 - f1: 0.6347
[0.4141227045031481, 0.83488375, 0.57311594, 0.7403401, 0.63472944]

```