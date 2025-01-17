# **Fine-Tuning модели BERT для Multi-Label классификации отзывов**

## Описание проекта

### Заказчик  
Samokat.Tech

### Исполнитель  
Мельник Даниил Владимирович

---

### **Описание**

#### **Цель**  

Разработать модель для классификации отзывов пользователей с возможностью присвоения нескольких меток (Multi-Label Classification). Модель должна учитывать пересечение тематик в тексте и предсказывать все затронутые классы.

**Основная метрика оценки** — **Accuracy**.  

Accuracy в задаче множественной классификации рассчитывается как доля полных совпадений между списком предсказанных и целевых классов:  

$$Accuracy = \frac{\text{Количество полных совпадений списков классов}}{\text{Общее количество экземпляров}}$$

#### **Задачи**  
1. Подготовить данные для обучения модели, включая обработку текстов и меток.  
2. Настроить процесс обучения модели на базе BERT с использованием методов Fine-Tuning.  
3. Реализовать метрику Accuracy для оценки точности модели в задаче множественной классификации.  
4. Обучить модель  
5. Оценить качество модели на тестовой выборке и подготовить файл предсказаний.  

---

### **Данные**

#### **Описание набора данных**  
Датасет состоит из текстов отзывов, тегов и соответствующих им меток классов.

#### **Файлы**
1. **train.csv**  
   Поля:  
   - `ID`: идентификатор экземпляра.  
   - `text`: текст отзыва.  
   - `tags`: метки (предварительные теги из анкеты).  
   - `trend_id_res0, trend_id_res1, ..., trend_id_res49`: метки по каждому из 50 классов (0 или 1).  

2. **test.csv**  
   Поля:  
   - `ID`: идентификатор экземпляра.  
   - `text`: текст отзыва.  
   - `tags`: метки (предварительные теги из анкеты).  

3. **trends_description.csv**  
   Поля:  
   - `trend_id`: идентификатор класса.  
   - `trend`: краткое название класса.  
   - `explanation`: подробное описание класса.

---

### **Технологический стек**  
- Python, NumPy, pandas  
- Transformers (Hugging Face)  
- PyTorch  
- scikit-learn  
- Matplotlib, Seaborn  

---

## Вывод

### **Ход работы**  

1. **Подготовка данных:**  
   - Изучены тексты отзывов и их метки.  
   - Проведена токенизация текстов с использованием модели BERT.   

2. **Обучение модели:**  
   - Были протестированы различные BERT-модели, в результате была выбрана `bert_base_bg_cs_pl_ru_cased`.  
   - Использован AdamW оптимизатор и обучение с линейным уменьшением learning rate (scheduler).  
   - Реализована ранняя остановка (Early Stopping) для предотвращения переобучения. 

| №  | Модель              | Batch Size (Train/Eval) | Warmup Steps | Weight Decay | Eval Loss          | Eval Accuracy       | Eval F1 Weighted       |
|----|---------------------|-------------------------|--------------|--------------|--------------------|---------------------|-------------------------|
| 1  | RoBERTa        | 50 / 50                | -            | 0.01         | -                  | -                   | -                       |
| 2  | RoBERTa         | 32 / 32                | -            | 0.01         | -                  | 0.412972972972973   | -                       |
| 3  | RoBERTa         | 16 / 64                | 500          | 0.01         | 0.0622814483940601 | 0.4097297297297297  | 0.5352045807404863      |
| 4  | DeBERTa        | 16 / 64                | 500          | 0.01         | 0.053661085665226  | 0.4962162162162162  | 0.6297241610458998      |
| 5  | DEBERTa        | 8 / 64                 | 500          | 0.01         | 0.0837200433015823 | 0.518918918918919   | 0.6794210524474236      |
| 6  | ALBERT Base v2  | 8 / 64                 | 500          | 0.01         | 0.0873901546001434 | 0.10054054054054054 | 0.15582162230049554     |
| 7  | DistilBERT   | 8 / 64                 | 500          | 0.01         | 0.07145585119724274| 0.46054054054054056 | 0.6196191350717499      |
| 8  | bert-base-multilingual | 8 / 64         | 500          | 0.01         | 0.0706319659948349 | 0.532972972972973   | 0.6919279418477221      |
| 9  | base-bg-cs-pl-ru-cased | 8 / 64        | 500          | 0.01         | 0.058454789221286774 | 0.5383783783783784 | 0.7042346808168742      |
| 10 | base-bg-cs-pl-ru-cased  | 4 / 64        | 500          | 0.01         | 0.06231588125228882 | 0.492972972972973   | 0.6534474904658384      |
| 11 | base-bg-cs-pl-ru-cased | 16 / 64       | 500          | 0.01         | 0.06396689265966415 | 0.5308108108108108  | 0.6873825334654116      |
| 12 | bert-base-multilingual | 16 / 64       | 500          | 0.01         | 0.05772503837943077 | 0.5308108108108108  | 0.6917886264070219      |
| 13 | base-bg-cs-pl-ru-cased + веса классов | 8 / 64     | 500          | 0.01         | 0.06049782410264015 | 0.5145945945945946  | 0.6797857023327455      |
| 14 | base-bg-cs-pl-ru-cased + веса классов  | 8 / 64      | 500          | 0.01         | 0.05954109877347946 | 0.4669603524229075  | 0.6204531972947426      |
| 15 | base-bg-cs-pl-ru-cased + веса классов | 8 / 64      | 500          | 0.02         | 0.06215649098157883 | 0.4779735682819383  | 0.6267315453298563      |
| 16 | base-bg-cs-pl-ru-cased + веса классов, размечаны пропущенные данные | 16 / 64      | 300          | 0.02         | 0.0580533929169178 | 0.5597874224977857  | 0.732149639693681      |
| 17 | base-bg-cs-pl-ru-cased + веса классов, сокращено количество объектов преобладающих классов | 16 / 64      | 300          | 0.02         | 0.057723816484212875 | 0.5006337135614702  | 0.7207890842047736      |
| 18 | base-bg-cs-pl-ru-cased + веса классов | 16 / 16      | 300          | 0.02         | 0.05449923500418663 | 0.5744870651204282  | 0.7302631210901074      |
| 19 | base-bg-cs-pl-ru-cased + веса классов | 16 / 16      | -          | 0.02         | 0.02920026145875454 | 0.722158438576349  | 0.6163953524156007      |

 

3. **Оценка модели:**  
   - Проведена кросс-валидация на обучающей выборке.  

---

### **Результаты**

#### **Метрика на валидационных данных**  
Accuracy: **0.723**.  

---

### **Выводы и рекомендации**  
- Использование модели BERT позволило справиться с задачей множественной классификации.  

- Для дальнейшего улучшения результатов можно:
  - Обучить модель на большем количестве эпох
  - Попробовать другие архитектуры моделей
  - Использовать ансамбль моделей  
  - Использовать аугментацию данных для увеличения обучающей выборки.  
  - Провести дополнительный анализ ошибок модели и уточнить разметку данных.  

---

