Проверка идей по созданию систем семантического поиска через использование классификаторов: 
- zero-shot
- few-shot (метод set-fit)

Имеется:
- набор комментариев, некоторые из которых, содержат описания какого-то проекта;
- небольшой размеченный набор текстов(100), в состав которого входит 8 текстов из положительного класса с меткой "1", а   
  остальные 82 тексты из класса - "0"

Задача: создать семантическую поисковую систему, которая сможет из разных наборов текстов извлекать тексты, 
содержащие описание проектов

Подход: zero-shot
Кратко суть идеи - используя значения множественной zero-shot классификации, создать вектор признаков, некий аналог word2vec:
class2vec или cluster2vec, в котором будет отражаться контекст класса или кластера текста, а значения вектора формируются 
через агрегацию значений zero-shot для выбранного в качестве базового набора слов-категорий.
В качестве основной модели будет использоваться mодели SBERT для классификации текстов, которые имеют встроенную zero-shot классификацию.
В качестве набора признаков будет использован список слов-категорий, близких к категории ПРОЕКТ:
list_words = ['project', 'proposal', 'job', 'solution', 'research', 'idea', 'algorithm', 'plan', 'initiative', 'announcement']

**Data:**
- labels.db - база данных SQLite с размеченнными 100 текстами соответствующие классу ПРОЕКТ (8-позитивных, 92 негативных)
- comments.json.gz - архивированный набор комментариев в формате HTML
- all_comments_texts.txt - список комментариев в текстовом формате, отобранный из comments.json.gz с длиной текста более 70 символов

**Список файлов:**
- zero-shot-idea.ipynb - предварительный этап: получение значений от двух SBERT моделей множественного zero-shot для 
  размеченного выбранного базиса слов   
- SetFit SST-2.ipynb - пример реализации метода SetFit
- set-fit-idea.ipynb - реализация решения через few-shot с использование библиотеки SetFit 

Черновики:
- start(draft).ipynb - черновик. проверка идей, гипотез, тестирование кода 
- dev.ipynb          - стартовая версия



