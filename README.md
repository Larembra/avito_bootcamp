# Search Retrieval Pipeline --- решение

Решение построено как классический ML-пайплайн поиска объявлений по
пользовательскому запросу.

Основной код решения находится в Jupyter Notebook:

``` text
search_retrieval_pipeline_v2.ipynb
```

## Требования

Рекомендуемая версия Python: **3.12**.

Установите зависимости:

``` bash
pip install -r requirements.txt
```

Также потребуется Jupyter Notebook или JupyterLab для запуска ноутбука.

## Расположение файлов

Перед запуском разместите все необходимые файлы в одной директории:

``` text
.
├── search_retrieval_pipeline_v2.ipynb
├── train.parquet
├── benchmark_items.parquet
├── benchmark_queries.parquet
├── requirements.txt
└── README.md
```

Файл `train.parquet` имеет размер около 500 МБ.

Ноутбук использует относительный путь к данным:

``` python
DATA_DIR = Path(".")
```

Поэтому запускать ноутбук нужно из директории, в которой находятся
parquet-файлы.

## Установка

Рекомендуемый порядок установки:

### 1. Установить Python 3.12

Проверьте версию:

``` bash
python --version
```

Должно быть:

``` text
Python 3.12.x
```

### 2. Установить зависимости

В директории проекта выполните:

``` bash
pip install -r requirements.txt
```

### 3. Запустить Jupyter

``` bash
jupyter notebook
```

или:

``` bash
jupyter lab
```

Откройте:

``` text
search_retrieval_pipeline_v2.ipynb
```

## Запуск решения

Выполните ячейки ноутбука **последовательно сверху вниз**.

Для полного режима решения используется:

``` python
FAST = False
```

В этом режиме используется полный набор retrieval-моделей, более
глубокий candidate pool и полный реранкинг.

Перед финальным запуском убедитесь, что присутствуют:

``` text
train.parquet
benchmark_items.parquet
benchmark_queries.parquet
```

## Результат

После выполнения ноутбука формируется итоговый файл:

``` text
submission_long.csv
```

Он содержит итоговое ранжирование benchmark-запросов:

``` text
query_id
item_id
rank
score
```

Также формируется файл с offline-метриками:

``` text
results_train_validation.csv
```

## Повторный запуск

Для воспроизводимого запуска:

1.  Используйте Python 3.12.
2.  Установите зависимости из `requirements.txt`.
3.  Разместите три parquet-файла рядом с ноутбуком.
4.  Запустите `search_retrieval_pipeline_v2.ipynb`.
5.  Выполните все ячейки сверху вниз.
6.  Используйте `FAST = False`.
7.  Получите `submission_long.csv`.

В ноутбуке зафиксирован `SEED = 42`, а промежуточные подготовленные
данные могут кэшироваться в `_prep_cache.pkl`.
