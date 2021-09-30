### Data Augmentation은 오히려 성능을 떨어뜨릴 수 있다.
글자 인식 문제에서, 글자 이미지를 좌우 또는 상하로 뒤집는 기법은 적당하지 않습니다.
글자가 지닌 의미가 왜곡될 가능성이 크기 때문이빈다.
심장을 촬영한 영상도 되집기 기법은 적절치 않습니다.

이미지가 지닌 의미를 바꾸지 않는 한에서 적용해야한다는 점을 주의해야 합니다.

이미지 내에 물체의 크기가 제각각이라면
이미지를 여러 크기로 자동 조절하는 기법이 큰 도움이 됩니다.
예로 의료 영상에서 환자마다 다른 장기 크기 사진에 적용하면 좋습니다.

그래서 augemntation 자동화를 하는 기법도 있습니다.
https://www.kakaobrain.com/blog/64 


# 
### Binary -> Category
1. 마지막 레이어의 activation
    tf.keras.layers.Dense(3, activation='softmax')  # sigmoid -> softmax
    
2. flow_from_directory() 사용 시 class_mode
  train_generator = training_datagen.flow_from_directory(
	TRAINING_DIR,
	target_size=(150,150),
	class_mode='categorical', # binary -> categorical 
  batch_size=126
)

3. compile의 loss
'categorical_crossentropy'는 one-hot 용
'sparse_categorical_crossentropy' 는 integer target 용
model.compile(loss = 'sparse_categorical_crossentropy', ~~)
