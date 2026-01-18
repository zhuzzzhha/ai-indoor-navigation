## Запуск проекта
Для сборки и запуска Docker контейнера необходимо последовательно выполнить следующие команды:
``` docker build -t ai-indoor-navigation```
``` docker run -it --name ai-indoor-container ai-indoor:latest /bin/bash```

## Запуск тестового примера
Для использования модели архитектуры **ResNet** необходимо запустить команду с нужными аргументами:

``` python source/ronin_resnet.py --mode test --test_list <path-to-train-list> --root_dir <path-to-dataset-folder> --out_dir <path-to-output-folder> --model_path <path-to-model-checkpoint>```

Модель архитектуры **LSTM**:

```python source/ronin_lstm_tcn.py test --type tcn --test_list <path-to-test-list> --data_dir <path-to-dataset-folder> --out_dir <path-to-output-folder> --model_path <path-to-model-checkpoint>```

## Сбор данных со смартфона
Собрать данные можно с помощью [приложения для Android](https://drive.google.com/file/d/1BVhfKE6FEL9YRO1WQCoRPgLtVixDbHMt/view) и выполнить их препроцессинг к [формату](https://ronin.cs.sfu.ca/README.txt)

## Обучение моделей
Обучение моделей можно выполнить с помощью команд:
```python source/ronin_resnet.py --mode train --train_list <path-to-train-list> --root_dir <path-to-dataset-folder> --out_dir <path-to-output-folder>```

```python source/ronin_lstm_tcn.py train --type tcn --config <path-to-your-config-file> --out_dir <path-to-output-folder> --use_scheduler```

## Оригинальная статья

**Paper**: [ICRA 2020](https://ieeexplore.ieee.org/abstract/document/9196860), [arXiv](https://arxiv.org/abs/1905.12853)  


### Citation 
[Herath, S., Yan, H. and Furukawa, Y., 2020, May. RoNIN: Robust Neural Inertial Navigation in the Wild: Benchmark, Evaluations, & New Methods. In 2020 IEEE International Conference on Robotics and Automation (ICRA) (pp. 3146-3152). IEEE.](https://ieeexplore.ieee.org/abstract/document/9196860)
