# 용어 정리
ex of Univariate time series
- Hour by hour temperature

ex of Multivariate time series
- Hour by hour weather 

Imputed data 
- A projection of unknown (usually past or missing) data

Seasonality
- A regular change in shape of the data

Trend
- An overall direction for data regardless of direction

Noise (in time series)
- Unpredictable changes in time series data

Autocorrelation
- Data that follows a predictable shape, even if the scale is different

Non-stationary time series
- One that has a disruptive event breaking trend and seasonality 

Window Dataset
- A fixed-size subset of a time series 




#
# Metrics for 성능 평가 

erros = forecasts - actual
- 제일 간단한 에러 계산식

mse = np.square(errors).mean()
- mean squared error
- 음수 값 제거를 위해 오차를 제곱하여 평균 계산

rmse = np.sqrt(mse)
- root mean squared error

mae = np.abs(errors).mean()
- mean absolute error
- 음수 값 제거를 위해 제곱이 아닌 절댓값 사용
- 그러면 mse보다 오류에 주는 불이익이 적음
- 이익과 손실이 오류의 크기에 비례하면 mae를 선호
- 그러나 큰 오류가 잠재적으로 위험하고, 작은 오류보다 훨씬 많은 비용이 든다면 mse를 선호
- keras.metrics.mean_absolute_error(x_valid, naive_forecast).numpy()

mape = np.abs(errors / x_valid).mean()
- mean absolute percentage error 
- 절댓값 에러와 절댓값 실제 값 사이 평균

# 
# Sequence Bias
Sequnce Bias는 선택이 항목 순서에 영향을 줄 때 생깁니다.

예를 들어 내가 좋아하는 TV 프로그램을 물어보고 "왕좌의 게임", "킬링 이브", "트래블러", "닥터 후"의 순서로 나열하면 '왕좌의 게임'을 선택할 가능성이 더 큽니다. '왕좌'는 여러분이 잘 알고 계시며 가장 먼저 보게 되는 것입니다. 다른 TV 프로그램과 동일하더라도. 따라서 데이터 세트의 데이터를 훈련할 때 시퀀스가 ​​비슷한 방식으로 훈련에 영향을 미치는 것을 원하지 않으므로 섞는 것이 좋습니다.

#
# 추가 설명

Question 7
If you want to inspect the learned parameters in a layer after training, what’s a good technique to use?
- Assign a variable to the layer and add it to the model using that variable. Inspect its properties after training

Question 9
If you want to amend the learning rate of the optimizer on the fly, after each epoch, what do you do?
- Use a LearningRateScheduler object in the callbacks namespace and assign that to the callback 

split an n column window into n-1 columns for features and 1 column for a label
- dataset = dataset.map(lambda window: (window[:-1], window[-1:]))

What does a Lambda layer in a neural network do?
- Allows you to execute arbitrary code while training
- axis parameter of tf.expand_dims  : Defines the dimension index at which you will expand the shape of the tensor 
- x data에는 batch_size, num of time series 뿐이라, RNN을 위해 series dimensionality를 추가하기 위해 이용
