
# Intro

Intro должно занять +-30 мин

## Общие вопросы ~ 10 min
- Побазарить за опыт
- Самая крутая фича которую делал за карьеру
- Как происходили процессы в команде. С кем общался, обговаривал требования, есть ли таск трекер, как выглядил цикл разработки, писал ли тесты
- Как выглядит твой обычный рабочий день.
Например: Дейлик, чекнул джиру + взял приоритетную задачи, напоролся на непонятный момент, поресерчил и по расспрашивал коллег / код ревью. А в конце дня закрыл таски в джире и создал пул реквест / запушил в свою ветку.
  
## Swift ~ 5 min
1) В чем плюсы Protocol-Oriented-Programming? Почему оно лучше Наследования в OOP?
Ответ: Нельзя наследовать несколько классов, с протоколами можно; протоколы можно расширять; лучше тестируется, разбивается на модули, более абстрактно

2) Зачем нам нужны делегаты в Swift? Где они используются?
Ответ: Повторное использование кода, изоляция логики. UIKit delegates, UIScrollView, UINavigationControllerDelegate, URLSessionDelegate кастомные делегаты

3) Че такое Optional? Зачем нужен? Как разворачивать?
Ответ: Безопасность, Явное указание на возможность отсутствия значения. !, if let, guard let, opationalValue?, ??

4) Различие guard let и if let
Ответ: Область видимости, Логика выхода

## UIKit ~ 5 min
5) Как ты верстал экраны? (Storyboard / Nib / Code / SwiftUI). Сможешь назвать минусы в работе со storyboard-дами?
Answer: Отсутствие переиспользуемости кода, Сложности при работе в команде, Производительность, Ограниченная масштабируемость, плохая гибкость

6) Как происходит оптимизация данных в TableView & CollectionView?
Ответ: Reuse Identifiers и использование dequeueReusableCell(withIdentifier:), UITableViewDataSourcePrefetching

7) В какой момент работы с UIKit-ом тебе приходится дергать layer у UIView?
Анимации, corners, borders, shadow

8) frame-based layout vs constraint-based layout, Что лучше?

## Git ~ 5 min
9) Для чего нам нужен гит?
для отслеживания изменений в коде и координации работы: ветвление и слияние, совместная работа, историческая справка, Резервное копирование, код-ревью

10) Какие гит команды знаешь?

11) pull vs fetch?
git fetch - обновляет информацию о ветках и коммитах из удаленного репозитория в ваш локальный репозиторий. Однако она не изменяет ваши локальные ветки и не сливает обновления с текущей рабочей веткой.
git pull делает две вещи одновременно:
- Выполняет git fetch, чтобы получить последние изменения из удаленного репозитория.
- Выполняет git merge / rebase

12) merge vs rebase?
- Создание истории:
Merge: Сохраняет полную историю изменений и создает новый коммит слияния.
Rebase: Переписывает историю коммитов, делая её линейной.
- История коммитов:
Merge: История веток остается разветвленной и отображается с коммитом слияния.
Rebase: История становится линейной, как если бы все изменения были сделаны последовательно.
- Конфликты:
Merge: Конфликты решаются только один раз в процессе слияния.
Rebase: Конфликты могут возникать несколько раз, так как каждый коммит переносится по очереди.
- Использование:
Merge: Лучше подходит для объединения веток, которые уже были опубликованы.
Rebase: Предпочтительнее для локальных веток перед публикацией, чтобы создать чистую и понятную историю.

13) Можно ли делать force push? В каких кейсах?
Исправление ошибок в истории коммитов, Очистка и упрощение истории перед слиянием: rebase -> force push

## Многопоточность ~ 3 min
14) Что такое GCD? Что такое очереди? В чем разница между concurrent и serial?
15) Расскажи где в проекте его использовал?
- Фоновая обработка работа с сетью / работа с диском / Обработка больших объемов данных 
- Параллельное выполнение задач
- Синхронизация для избежания проблем
- Отложенные задачи DispatchQueue.main.asyncAfter
- DispatchGroup
