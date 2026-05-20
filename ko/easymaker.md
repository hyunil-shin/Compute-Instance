## Machine Learning > AI EasyMaker > 콘솔 사용 가이드

## 노트북

머신 러닝 개발을 위한 필수 패키지가 설치되어 있는 주피터(Jupyter) 노트북을 생성하고 관리합니다.

### 노트북 목록

노트북의 상태가 표시됩니다. 주요 상태는 아래 표를 참고하세요.

| 상태               | 설명                                                                                                                              |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | 노트북 생성이 요청된 상태입니다.                                                                                                  |
| CREATE IN PROGRESS | 노트북 인스턴스를 생성 중인 상태입니다.                                                                                           |
| ACTIVE (HEALTHY)   | 노트북 애플리케이션이 정상적으로 구동 중인 상태입니다.                                                                            |
| ACTIVE (UNHEALTHY) | 노트북 애플리케이션이 정상적으로 구동되지 않은 상태입니다. 노트북을 재시작한 후에도 이 상태가 지속되면 고객지원으로 문의하세요. |
| STOPPED            | 노트북을 중지한 상태입니다.                                                                                                       |

### 텐서보드 활용을 위한 지표 로그 저장

학습 후 텐서보드 화면에서 결과 지표를 확인하기 위해, 학습 스크립트 작성 시 텐서보드 로그 저장 공간을 지정된 위치(`EM_TENSORBOARD_LOG_DIR`)로 설정해 주어야 합니다.

<details>
<summary><strong>예시</strong></summary>

```python
import tensorflow as tf

# 텐서보드 로그 경로 지정
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # 모델 구현

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

### 하이퍼파라미터 입력 화면

![하이퍼파리미터 입력 화면](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)
