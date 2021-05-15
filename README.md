# Avito-Category-Prediction
Kaggle-соревнование, требующее построить модель, предсказывающую к какому одному из 50 классов относится объявление, на основе более чем 4,5 млн данных. Датасет содержит заголовок объявления, его описание и класс. Разработала модель классификации объявлений авито на 50 категорий с применением модели fasttext
Проверяется несколько моделей с различными подходами к решению задачи
1. Был проведен разведовочный анализ, в тексте заполнены пропуски, визуализировано соотношение классов в датасете. Для экономии доступной ОЗУ было выбрано 500к слуайных объектов в датасете
2. 
3. Реализовала кастомный токенизатор, лемматизирующий текст, очищающий текст от стоп-слов и пунктуации
4. Использовала SVD-сжатие для применение LightGBM-модели. Обучила классические модели МО: LogReg, SGD
5. Обучила fasttext модель с биграммами на всем корпусе текстов. Использовала предобученную fasttext-модель для
векторизации текста, обучила модель fasttext на эмбеддингах
