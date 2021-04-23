# B-Tree

[![CMake](https://github.com/Sungatullin/semester-work-b-tree-006/actions/workflows/cmake.yml/badge.svg)](https://github.com/Sungatullin/semester-work-b-tree-006/actions/workflows/cmake.yml)

- Структура данных - **B-tree**
- **B-tree** - сильноветвящееся сбалансированное дерево поиска. Они созданы специально для эффективной работы с дисковой памятью.
- **B-tree** имеет следующие свойства (**t** — параметр дерева, называемый минимальной степенью B-tree, не меньший **2**.):
  - Каждый узел содержит хотя бы один ключ. Корень содержит от **1** до **2t-1** ключей. Любой другой узел содержит от **t-1** до **2t-1** ключей. Листья не являются исключением из этого правила.
  - У листьев потомков нет. Любой другой узел, содержащий **n** ключей, содержит **n+1** потомков. При этом:
    - Первый потомок и все его потомки содержат ключи из интервала **(-∞; K<sub>1</sub>)**;
    - Для **2≤i≤ n**, **i**-й потомок и все его потомки содержат ключи из интервала **(K<sub>i-1</sub>; K<sub>i</sub>)**;
    - **(n+1)**-й потомок и все его потомки содержат ключи из интервала **(K<sub>n</sub>; ∞)**.
  - Глубина всех листьев одинакова.
- **Операции**:
  - Поиск ключа - **O(tlog<sub>t</sub>n)**
  - Добавление ключа - **O(tlog<sub>t</sub>n)**
  - Разбиение узла
  - Удаление ключа - **O(tlog<sub>t</sub>n)**
    - Удаление ключа из листа
    - Удаление ключа из внутреннего узла
    - Перемещение ключа
    - Слияние
- **B-Tree** широко используется в базах данных и файловых системах (например: NTFS, HFS+, ext4) 

## Wolf's

| Фамилия Имя   | Вклад (%) | Прозвище              |
| :---          |   ---:    |  ---:                 |
| Илья Калимуллин   | 33,3        |  _ilya_               |
| Булат Сунгатуллин   | 33,3        |  _bulat_ |
| Паша Шумбасов   | 33,3        |  _pasha_         |

**Девиз команды**
> _В этой жизни ты либо волк, либо не волк☝_

## Структура проекта

Проект состоит из следующих частей:

- [`src`](src)/[`include`](include) - реализация структуры данных (исходный код и заголовочные файлы);
- [`benchmark`](benchmark) - контрольные тесты производительности структуры данных (операции добавления, удаления,
  поиска и пр.);
- [`examples`](examples) - примеры работы со структурой данных;
- [`dataset`](dataset) - наборы данных для запуска контрольных тестов и их генерация;

## Требования (Prerequisites)

Рекомендуемые требования:

1. С++ компилятор c поддержкой стандарта C++17 (например, _GNU GCC 8.1.x_ и выше).
2. Система автоматизации сборки _CMake_ (версия _3.12.x_ и выше).
3. Интерпретатор _Python_ (версия _3.7.x_ и выше).
4. Рекомендуемый объем оперативной памяти - не менее 4 ГБ.
5. Свободное дисковое пространство объемом ~ 3 ГБ (набор данных для контрольных тестов).

## Сборка и запуск

### Пример (Windows)

#### Сборка проекта
- 1 способ:
  - Склонируйте проект к себе на устройство через [Git for Windows](https://gitforwindows.org/) (либо используйте возможности IDE):
  ```shell
  git clone https://github.com/Algorithms-and-Data-Structures-2021/semester-work-b-tree-006.git
  ```
  ![](img/git_clone.png)
- 2 способ:
  - Откройте проект в [CLion](https://www.jetbrains.com/ru-ru/clion/), используя URL:
  ```shell
  https://github.com/Algorithms-and-Data-Structures-2021/semester-work-b-tree-006.git
  ```
  ![](img/path_to_project2.png)
  
#### Генерация тестовых данных

Генерация тестового набора данных в
формате [Text file(TXT)](https://en.wikipedia.org/wiki/Text_file):

- Процесс генерации тестовых данных:
  - откройте проект в [CLion](https://www.jetbrains.com/ru-ru/clion/)
  ![](img/path_to_project2.png | width=250)
  <img src="https://camo.githubusercontent.com/..." data-canonical-src="img/path_to_project2.png" width="200" height="400" />
  - определите путь до проекта
  ![](img/path_to_project.png)
  - пропишите максимальное значение элементов(по желанию)
  ![](img/max_rand.png)
  - запустите **generate_csv_dataset.cpp**
  ![](img/run_generater.png)
  - подождите пока сгенерируются все данные
  ![](img/finish_generation.png)

Тестовые данные представлены в TXT формате (см.
[`dataset/data/dataset-example.txt`](dataset/data/dataset-example.txt)):

```txt
654
44
78
132
256
...
```

**Примечание**. Данные для удобства запуска контрольных тестов организовываются так:

```shell
dataset/data/
  add/
    01/
      100.txt
      ...
      5000000.txt
    02/ ...
    03/ ...
    ...
    10/ ...
  search/
    01/
      100.txt
      ...
      5000000.txt
    ...
    10/ ...
  ...
```

По названию директории `/dataset/data/add` можно понять, что здесь хранятся наборы данных для контрольных тестов по
**добавлению** элементов в структуру данных. Названия файлов `100.txt`. `5000000.txt` и т.д. хранят информацию о размере набора данных (т.е. количество элементов). 

#### Контрольные тесты (benchmarks)

_Опишите, как запустить контрольные тесты, что они из себя представляют, какие метрики замеряют (время работы,
потребление памяти и пр.)._

Для запуска контрольных тестов необходимо предварительно сгенерировать или скачать готовый набор тестовых данных.

**Примечание**. Во избежание "захламления" репозитория большим объёмом данных рекомендуется указать ссылку на архив с
набором данных, который при необходимости можно скачать по ссылке. Наборы данных должны находиться в папке семестровой
работы на [Google Drive](https://drive.google.com/drive/folders/17-qridbMXFnz3E-6UjOj0WD1H0jWtpz3?usp=sharing).

##### Список контрольных тестов

| Название                  | Описание                                | Метрики         |
| :---                      | ---                                     | :---            |
| `random_search_benchmark` | поиск элементов по случайному индексу   | _время_         |
| `add_benchmark`           | добавление элементов в структуру данных | _время, память_ |
| ...                       | ...                                     | ...             |

##### Примеры запуска

```shell
./benchmark <input> <output> --trials 50
```

- `<input>` - входной файл с набором данных в формате CSV;
- `<output>` - выходной файл с результатами контрольного теста;
- `--trials` - количество прогонов на наборе данных и т.д.

Добавление 10000 случайных элементов в структуру данных (повторить операцию 50 раз и вычислить среднее время работы и
потребляемую память):

```
./add_benchmark.exe ../dataset/data/add/10000.csv metrics.txt --trials 50
``` 

где `<input> = ../dataset/data/add/10000.csv` и `<output> = metrics.txt`.

**Примечание**. Файл с метриками не обязателен, можете выводить данные в стандартный поток вывода (т.е. консоль).

## Источники

_Список использованных при реализации структуры данных источников._

_**Это не плагиат, это уважение чужого труда и помощь своим сокурсникам более подробно разобраться в теме.**_

