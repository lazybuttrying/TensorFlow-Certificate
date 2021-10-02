# Metrics for 

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
