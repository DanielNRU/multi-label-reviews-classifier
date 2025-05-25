# 🤖 Multi-Label Reviews Classifier (BERT Fine-Tuning)

[![Python](https://img.shields.io/badge/python-3.10-blue)](https://www.python.org/) [![PyTorch](https://img.shields.io/badge/pytorch-2.0+-red)](https://pytorch.org/) [![Transformers](https://img.shields.io/badge/transformers-4.30+-yellow)](https://huggingface.co/docs/transformers/index) [![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)

> **Многоуровневая классификация отзывов пользователей с помощью BERT и современных ML-практик**

---

<table>
<tr>
<td width="120"><img src="https://habrastorage.org/getpro/moikrug/uploads/company/100/007/329/0/logo/big_77df337bb1f61c4628e55b540ac327ab.png" width="100" alt="ecom.tech Logo"></td>
<td>
<b>Заказчик:</b> <a href="https://samokat.tech/">ecom.tech (ex. Samokat.tech)</a> — технологическая компания, развивающая сервисы для e-commerce и ритейла.
</td>
</tr>
</table>

---

## 📋 Оглавление

* [О проекте](#-о-проекте)
* [Ключевые возможности](#-ключевые-возможности)
* [Архитектура и стек технологий](#-архитектура-и-стек-технологий)
* [Требования](#-требования)
* [Рекомендации по улучшению](#-рекомендации-по-улучшению)
* [Структура проекта](#-структура-проекта)
* [Контакты и поддержка](#-контакты-и-поддержка)

---

## 🔍 О проекте

Multi-Label Reviews Classifier — это система для автоматической классификации пользовательских отзывов с возможностью присвоения сразу нескольких тематических меток (multi-label). В основе лежит дообученная модель BERT, адаптированная под специфику текстов и классов заказчика.

**Задача:** повысить точность автоматической разметки отзывов, учитывая, что один отзыв может относиться к нескольким категориям одновременно.

**Метрика:** Accuracy = доля полных совпадений списков классов между предсказанием и эталоном.

---

## 🚀 Ключевые возможности

* 🏷️ **Мульти-классовая классификация:** поддержка 50 тематик для одного отзыва
* 🤖 **Fine-Tuning BERT:** адаптация предобученной модели под задачу заказчика
* 🧮 **Современные ML-практики:** AdamW, scheduler, ранняя остановка (Early Stopping)
* 📊 **Валидация и отчётность:** кросс-валидация, автоматический подсчёт метрик
* 📈 **Улучшение метрики:** прирост Accuracy с 0.5 до 0.723 на валидации
* 🛠️ **Гибкая архитектура:** легко расширяется под новые классы и данные

---

## 🏗 Архитектура и стек технологий

**Стек:** Python 3.10+, PyTorch, HuggingFace Transformers, scikit-learn, pandas, numpy

| Компонент         | Технологии                                  |
| ----------------- | ------------------------------------------- |
| Модель            | BERT (`bert_base_bg_cs_pl_ru_cased`)        |
| ML-фреймворк      | PyTorch, Transformers (HuggingFace)         |
| Данные            | pandas, numpy                               |
| Метрики/валидация | scikit-learn                                |
| Визуализация      | matplotlib, seaborn                         |

---

## 📋 Требования

* Python >= 3.10
* PyTorch >= 2.0
* transformers >= 4.30
* pandas, numpy, scikit-learn, matplotlib, seaborn

---

## 🛠 Рекомендации по улучшению

- Увеличить число эпох обучения
- Попробовать другие архитектуры (RoBERTa, DeBERTa)
- Использовать ансамбли моделей
- Применить аугментацию данных
- Провести анализ ошибок и уточнить разметку

---

## 📁 Структура проекта

```
multi-label-reviews-classifier/
├── model/                      # Файлы модели и токенизатора (config.json, model.safetensors, tokenizer.json, vocab.txt и др.)
├── NLP_Samokat_bert.ipynb      # Основной ноутбук с кодом обучения и инференса
├── submission.csv              # Файл с предсказаниями модели
└── README.md                   # Документация по проекту
```

---

## ✉️ Контакты и поддержка

**Автор:** Мельник Даниил

* Email: [git@danieln.ru](mailto:git@danieln.ru)
* GitHub: [DanielNRU](https://github.com/DanielNRU)

--- 