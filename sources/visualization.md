
## 모델 시각화

Keras는 모델을 시각화하기 위한 `graphviz`기반 유틸리티 함수들을 제공합니다.

아래의 코드는 모델의 그래프를 그려주고, 이미지를 파일로 저장해 줍니다.

```python
from keras.utils import plot_model
plot_model(model, to_file='model.png')
```

`plot_model`에서는 다음 네 개의 인자를 지정할 수 있습니다.

- `show_shapes` (기본값: False) controls whether output shapes are shown in the graph.
- `show_layer_names` (기본값: True) controls whether layer names are shown in the graph.
- `expand_nested` (기본값: False) controls whether to expand nested models into clusters in the graph.
- `dpi` (기본값: 96) controls image dpi.

You can also directly obtain the `pydot.Graph` object and render it yourself,
for example to show it in an ipython notebook :
```python
from IPython.display import SVG
from keras.utils import model_to_dot

SVG(model_to_dot(model).create(prog='dot', format='svg'))
```

## Training history visualization

The `fit()` method on a Keras `Model` returns a `History` object. The `History.history` attribute is a dictionary recording training loss values and metrics values at successive epochs, as well as validation loss values and validation metrics values (if applicable). Here is a simple example using `matplotlib` to generate loss & accuracy plots for training & validation:

```python
import matplotlib.pyplot as plt

history = model.fit(x, y, validation_split=0.25, epochs=50, batch_size=16, verbose=1)

# Plot training & validation accuracy values
plt.plot(history.history['acc'])
plt.plot(history.history['val_acc'])
plt.title('Model accuracy')
plt.ylabel('Accuracy')
plt.xlabel('Epoch')
plt.legend(['Train', 'Test'], loc='upper left')
plt.show()

# Plot training & validation loss values
plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])
plt.title('Model loss')
plt.ylabel('Loss')
plt.xlabel('Epoch')
plt.legend(['Train', 'Test'], loc='upper left')
plt.show()
```
