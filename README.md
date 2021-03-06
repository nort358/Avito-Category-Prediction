# Avito-Category-Prediction
Kaggle-соревнование, требующее построить модель, предсказывающую к какому одному из 50 классов относится объявление, на основе более чем 4,5 млн данных. Датасет содержит заголовок объявления, его описание и класс. Разработано с применением модели fasttext с результатом f1-score = 0.9
Проверяется несколько моделей с различными подходами к решению задачи:
1. Был проведен разведовочный анализ, в тексте заполнены пропуски, визуализировано соотношение классов в датасете. Для экономии доступной ОЗУ было выбрано 500к слуайных объектов в датасете
2. Для того, чтобы объединить предобработку текста и токенизацию, разработан кастомный токенизатор-preprocessor, объединяющий функции NLTK и pymorphy2 для лемматизации текста. Текст очищен от пунктуации стоп-слов. Реализация составила ~4 минуты на 100к строк
3. Обучила классические модели МО: LogReg, SGD. Результат accuracy составил 0.82 и 0.77 сответственно. Для логистической регрессии использовался описк по сетке с перебором параметров регуляризации и С
4. Использовала SVD-сжатие до размерности векторов = 500 для применение LightGBM-модели. Доля объясненной дисперсии составила 0.4, accuracy на модели градиентного бустинга - 0.81
5. Для дальнейшего применения модели fasttext размер батча был увеличен до 1кк благодаря оптимальной рализации библиотеки.
6. Данные были обработаны с помощью библиотеки gensim и преобразованы в txt файл, чтобы передать их модели для обучения. Разница модели без автотюна на отложенной выборки и с автоюном составила 0.02 в f1-score. Конечный результат: 0.88 и 0.9 на валидайционных данных
7. Обучение fasttext модели на всем корпусе текстов на стороннем устройстве не дало прироста в качестве. 
8. Использование предобученной fasttext-модели потребовало преобразование .bin модели в .vec формат файла, идея transfer learninga не показала никакого результата, он вышел хуже, чем использование модели без предварительного обучения на русской части википедии, которое предоставляет библиотека fasttext. f1-score в этом случае был равен 0.88
9. Использование бибилиотеки для создания embedding'ов и последующем обучении SGD и LightGBM показало результаты 0.74 и 0.68 f1-score соответственно

Лучшие результаты были получены на батче размером 1кк на не предобученной fasttext модели с автотюном. Результат в kaggle-соревновании - 0.89774 accuracy на приватной части
