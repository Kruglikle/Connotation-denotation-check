# Connotation-denotation-check
Multilevel analysis of word denotation and connotations (including inherent: evaluative, emotive, expressive, stylistic) and bonus :)) - irony features using NLP models.

Работа кода:

Проепроцессинг: 
Программа получает текст
Токенизация и фильтрация стоп-слов
Текст разбивается на отдельные слова с помощью nltk.word_tokenize.
Стоп-слова (например, “the”, “and”) удаляются, чтобы не мешали анализу (но потом мы про это забыли)), поэтому код пока вдоработке. стоп-слова уберем, обещаем!)

Основной код:
1. Определение денотата (denoatation, WordNet)
Для каждого слова ищется определение в WordNet (wn.synsets(word)[0].definition()), которое даёт прямое значение слова.

2. Оценочная коннотация (evaluative, VADER)
Каждое слово анализируется через SentimentIntensityAnalyzer из NLTK.
Выдается классификация Positive, Negative или Neutral по тональности слова.

3. Эмоциональная коннотация (emotive, GoEmotions)
Каждое слово передаётся модели GoEmotions (bert-base-go-emotion) для определения эмоции (anger, joy, sadness и т.д.) с вероятностью.

4. Экспрессивная коннотация (expressive)
Берётся из оценки тональности (evaluative): если evaluative != Neutral, слово считается Expressive, иначе Not expressive.

5. Стилистическая коннотация (stylistic, s-nlp/xlmr_formality_classifier)
Каждое слово классифицируется как Formal, Informal или Neutral.

На днях сделаю, чтобы все результаты сохранялись в Pandas DataFrame и могли экспортироваться в CSV/excel
