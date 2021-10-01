# IBMD Review
- 전체 50000개 중 train 25000, test 25000로 50/50 비율
- IBMD suvwords는 8000개

# Overfitting on NLP
valid_set에 어휘가 거의 없기에 ovefitting이 쉽게 발생. 이는 분류할 수 없고 overfitting으로 인한 여러 문제를 겪게 됨

# One LSTM vs Two LSTM
- one LSTM
  - tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(64, return_sequences=True)),
- two LSTM
   - tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(64, return_sequences=True)),
   - tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(32)),

- training accuracy 그래프는 one LSTM에서 들쭉날쭉
- loss 그래프에서는 처음 10 epoch 동안 비슷하다가, 50 epoch까지 진행해보면 푹 꺼지는 지점들이 종종 생김.
- 특히 one LSTM이 two LSTM보다 몇 번 더 푹 꺼진다
- 이를 해결할 수 있는 방법으로 LSTM()을 지우고 그 자리에 아래 방법을 선택하여 두 줄을 적는 것이다
  - 1. Flatten(), GlobalAveragePooling1D()를 이용해 평평하게 한다
    - 이는 LSTM을 적용해서 생긴 overfitting을 제거하기도
  - 2. Conv1D, GlobalMaxPooling1D()를 이용
    - 단어는 필터의 크기로 그룹화 된다.
    - Conv1D(128,5, activation='relu') : 5개의 단어마다 128개의 필터를 보유
    - 입력의 최대 길이가 120일 때 5개 단어에 대해 구성하면, 앞뒤로 두 단어씩 잘라내어 116이 남음
    - 128개의 필터는 conv의 2차원 크기로 정해짐
    - embedding (120,16) -> conv1d (116,128) -> maxpool (128)
