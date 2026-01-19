## Сбор данных со смартфона
Данные IMU можно собрать, используя [SensorLogger](https://www.tszheichoi.com/sensorlogger), доступное для ([Android](https://play.google.com/store/apps/details?id=com.kelvin.sensorapp[) и [iOS](https://apps.apple.com/us/app/sensor-logger/id1531582925)).


## Сборка проекта
Для сборки и запуска Docker контейнера необходимо последовательно выполнить следующие команды:
``` docker build -t ai-indoor-navigation .```
``` docker run -it --rm --name ai-indoor-container ai-indoor-navigation:latest /bin/bash```

## Загрузка моделей
Чекпоинты обученных моделей доступны [здесь](https://www.frdr-dfdr.ca/repo/dataset/816d1e8c-1fc3-47ff-b8ea-a36ff51d682a)

## Получение траектории из данных SensorLogger
В запущенном контейнере выполните команду
```python3 source/run_from_sensorlogger.py --path <sensor_logger_data> --model_path ronin_resnet/checkpoint_gsn_latest.pt```


Полученные данные должны быть в следующем формате:
  * `Gyroscope.csv`
  * `Orientation.csv`
  * `Acceleration.csv`

При использовании других приложений для сбора данных необходимо конвертировать их в описанный формат.

### Gyroscope.csv:
```
time,seconds_elapsed,z,y,x
1718030736872695300,0.0706953125,-0.32157647609710693,0.15512901544570923,0.6729803085327148
```

### Orientation.csv:
```
time,seconds_elapsed,qz,qy,qx,qw,roll,pitch,yaw
1718030736912338000,0.110337890625,-0.49317896366119385,-0.10824661701917648,0.21374563872814178,0.8362834453582764,0.033629775047302246,-0.4828145205974579,1.0739439725875854
```
NOTE: roll, pitch, and yaw are not required by RoNIN

### Acceleration.csv:
```
time,seconds_elapsed,z,y,x
1716979893874983200,0.047983154296875,9.851848602294922,1.407876968383789,-0.008374879136681557
```

## Запуск тестового примера на данных открытого датасета
Для использования модели архитектуры **ResNet** необходимо запустить команду с нужными аргументами:

``` python source/ronin_resnet.py --mode test --test_list <path-to-train-list> --root_dir <path-to-dataset-folder> --out_dir <path-to-output-folder> --model_path ronin_resnet/checkpoint_gsn_latest.pt```

Модель архитектуры **LSTM**:

```python source/ronin_lstm_tcn.py test --type tcn --test_list <path-to-test-list> --data_dir <path-to-dataset-folder> --out_dir <path-to-output-folder> --model_path <path-to-model-checkpoint>```

## Обучение моделей
Обучение моделей можно выполнить с помощью команд:
```python source/ronin_resnet.py --mode train --train_list <path-to-train-list> --root_dir <path-to-dataset-folder> --out_dir <path-to-output-folder>```

```python source/ronin_lstm_tcn.py train --type tcn --config <path-to-your-config-file> --out_dir <path-to-output-folder> --use_scheduler```

## Оригинальная статья

**Paper**: [ICRA 2020](https://ieeexplore.ieee.org/abstract/document/9196860), [arXiv](https://arxiv.org/abs/1905.12853)  


### Citation 
[Herath, S., Yan, H. and Furukawa, Y., 2020, May. RoNIN: Robust Neural Inertial Navigation in the Wild: Benchmark, Evaluations, & New Methods. In 2020 IEEE International Conference on Robotics and Automation (ICRA) (pp. 3146-3152). IEEE.](https://ieeexplore.ieee.org/abstract/document/9196860)
