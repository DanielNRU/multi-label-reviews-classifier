# **Fine-Tuning модели BERT для Multi-Label классификации отзывов**
---

Этот проект посвящён разработке модели для классификации отзывов пользователей с возможностью присвоения нескольких меток (Multi-Label Classification) с использованием моделей BERT. Основной задачей является создание модели, которая будет учитывать пересечение тематик в тексте и точно предсказывать все затронутые классы.

## Оглавление

1. [Описание проекта](#описание-проекта)  
2. [Особенности реализации](#особенности-реализации)  
3. [Данные](#данные)  
4. [Технологический стек](#технологический-стек)  
5. [Ход работы](#ход-работы)  
6. [Результаты](#результаты)  
7. [Рекомендации по улучшению](#рекомендации-по-улучшению)   
8. [Контакты](#контакты)  

---
## Заказчик
[ecom.tech (ex. Samokat.tech)](https://samokat.tech/) 

## Описание проекта

В рамках проекта была разработана модель для классификации отзывов пользователей с множественными метками. Модель использует архитектуру BERT и применяет метод Fine-Tuning для адаптации модели под задачу многоклассовой классификации. Основная цель — достичь улучшения метрики точности (Accuracy) с учетом множественных меток на один текст отзыва.

$$Accuracy = \frac{\text{Количество полных совпадений списков классов}}{\text{Общее количество экземпляров}}$$

На момент начала работы над проектом, текущая метрика Accuracy составляла **0.5**.

## Особенности реализации

- **Модель BERT**: используется предобученная модель BERT с дообучением на текстах отзывов с множественными метками.  
- **Fine-Tuning**: для настройки модели использован метод Fine-Tuning с оптимизатором AdamW и scheduler'ом для уменьшения learning rate.  
- **Метрика**: для оценки производительности модели использовалась метрика Accuracy, рассчитываемая как доля полных совпадений предсказанных и целевых классов.  
- **Раннее прекращение (Early Stopping)**: для предотвращения переобучения модели был применен механизм ранней остановки.

## Данные

Данные состоят из текстов отзывов, меток классов и других дополнительных полей, которые обеспечивают полноценное представление задачи.

### Файлы

1. **train.csv**  
   Поля:
   - `ID`: уникальный идентификатор экземпляра.
   - `text`: текст отзыва.
   - `tags`: метки (предварительные теги).
   - `trend_id_res0, trend_id_res1, ..., trend_id_res49`: метки по каждому из 50 классов.

2. **test.csv**  
   Поля:
   - `ID`: идентификатор экземпляра.
   - `text`: текст отзыва.
   - `tags`: метки.

3. **trends_description.csv**  
   Поля:
   - `trend_id`: идентификатор класса.
   - `trend`: название класса.
   - `explanation`: подробное описание класса.

## Технологический стек

- Python, NumPy, pandas  
- Transformers (Hugging Face)  
- PyTorch  
- scikit-learn  
- Matplotlib, Seaborn  

## Ход работы

1. **Подготовка данных**:  
   - Изучены тексты отзывов и их метки.  
   - Применена токенизация текстов с использованием модели BERT для преобразования текстов в формат, пригодный для обучения.

2. **Обучение модели**:  
   - Использованы несколько вариантов модели BERT, среди которых была выбрана `bert_base_bg_cs_pl_ru_cased` как наиболее подходящая.  
   - Применены методы оптимизации: оптимизатор AdamW и линейное уменьшение learning rate.  
   - Введен механизм ранней остановки для предотвращения переобучения.

3. **Оценка модели**:  
   - Проведена кросс-валидация на обучающей выборке для оценки стабильности модели.

## Результаты

**Метрика на валидационных данных**  
- После fine-tuning модель достигла значения Accuracy **0.723**, что представляет собой улучшение на **44.6%** по сравнению с исходной метрикой.

## Рекомендации по повышению качества модели

Для дальнейшего улучшения результатов можно:
- Обучить модель на большем количестве эпох.
- Применить другие архитектуры моделей, такие как RoBERTa или DeBERTa.
- Использовать ансамбль моделей для повышения точности.
- Применить аугментацию данных для увеличения объема обучающей выборки.
- Провести дополнительный анализ ошибок модели и уточнить разметку данных.

## Контакты

Если у вас есть вопросы, предложения или обратная связь, свяжитесь со мной:  

- **Имя**: Даниил Мельник  
- **Email**: git@danieln.ru  
- **GitHub**: [DanielNRU](https://github.com/DanielNRU)  

--- 