# Руководство по управлению библиотеками ГПБ

## Введение

Согласно [процесса управления библиотеками в ГПБ](/docs/swamp.libraries_management_process) у нас есть несколько типов библиотек требующих управления. Данная инструкция предназначена для описания шагов, которые нужно выполнить, чтобы описать конкретный тип библиотеки в DocHub.

## Правила оформления репозитория библиотеки и публикации релизов

Для типов библиотек, которые размещаются в системе контроля версий ГПБ должны выполняться следующие требования:
* Должен быть описан `README.md` с:
  * Общим описанием и назначением библиотеки
  * Инструкцией по установке и использованию
  * Примерами использования (опционально)
* При именовании библиотеки, рекомендуется следовать общепринятому подходу в стеке библиотеки.
* Для версионирования библиотеки необходимо следовать спецификации [Семантического Версионирования](https://semver.org/).
* Новые версии библиотеки необходимо публиковать с использование функционала "Релизы" в GitLab.
  * Описать Release notes с ключевыми изменениями релиза.
  * Создать тег равный версии в основном манифесте существующего стека (например, `setup.py` для Python или `package.json` для JavaScript).
* Уведомлять заинтересованных лиц о появлении новых версий библиотеки.

## Зеркалирование библиотеки

Раздел находится в проработке

## Правила описания библиотек компании в DocHub

В данном разделе описаны основные правила описания библиотек в DocHub. При этом нужно учитывать, что инструмент DocHub постоянно развивается и часть информации может быть неактуальной. С целью минимизации таких ситуаций описание происходит на достаточно высоком уровне.

### Структура данных для управления библиотеками

На момент актуализации инструкции была принята следующая структура данных для управления библиотеками:
1. Все библиотеки описываются только в репозитории
2. Описание библиотек хранится в репозитории по следующему пути: `./application_arch/libraries`
3. Внутри папки `libraries` хранятся yaml файлы описывающие конкретные библиотеки

### Правила именования объектов связанных с библиотеками

1. Все имена, названия и код должны писаться в нотации [snake_case](https://ru.wikipedia.org/wiki/Snake_case)
2. Имя yaml файла описывающего конкретную библиотеку должно соответствовать идентификатору библиотеки
3. Идентификатор библиотеки в общем случае представляет из себя имя в виде `<имя библиотеки>`

### Правила описания библиотеки

Описание библиотек должно выполняться на основании шаблона ./libraries/template/library_template.yaml. Для этого необходимо:
1. Скопировать шаблон из каталога ./libraries/template
2. Переименовать шаблон yaml файл в имя будущей библиотеки
3. Сделать импорт вашего файла внутри `./application_arch/libraries/_root.yaml`
```yaml
imports:  
  - django_catalog.yaml
  - sign_django_sdk.yaml
  - swamp_ui.yaml
```
4. Указать в идентификаторе библиотеки имя новой библиотеки соответствующее имени yaml файла
5. Заполнить все остальные данные по библиотеке согласно инструкции внутри шаблона
7. Проверить, что ваша система корректно была заимпортирована. Для этого нужно открыть в IDE редактор JSONata и выполнить запрос, например: `libraries."django_catalog"`
![](images/libraries_jsonata.png)

### Правила привязывания библиотеки к системе

Основной целью описания библиотеки является получение понимания того, какие библиотеки в компании уже есть и в каких системах они используются. Для достижения этой цели, при описании системы нужно добавлять используемые библиотеки. Для этого необходимо открыть файл описывающий систему и добавить:
```yaml
libraries:
  - sign_django_sdk
  - swamp_ui
```

### Инструкция по работе с библиотеками на портале DocHub

На момент написания инструкции реализовано несколько инструментов для работы с библиотеками

#### Каталог библиотек

Каталог библиотек служит для того чтобы понять какие библиотеки существуют в компании и для чего они используются. Для открытия каталога необходимо перейти в меню `Прикладная архитектура -> 12. Библиотеки -> 01. Каталог библиотек` или набрать в поиске `Каталог библиотек`.
![](images/libraries_list.png)

#### Список библиотек в системах

Для того чтобы понять в каких системах какие библиотеки используются есть специальный отчет `Прикладная архитектура -> 12. Библиотеки -> 02. Список библиотек в системах`.

Если вам нужно посмотреть все библиотеки по конкретной системе, то нужно нажать в колонке фильтр `Отбор по системе`.
![](images/sys_libraries_list.png)


#### Карточка библиотеки

Для того чтобы посмотреть детальные параметры по конкретной библиотеки нужно нажать ссылку на имени библиотеки в одном из отчетов выше.

Помимо всей информации, которая есть в yaml-файле с описанием библиотеки в карточке выводится список систем в которых используется выбранная библиотека.
![](images/library_card.png)
