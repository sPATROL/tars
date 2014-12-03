Файловая структура
==================

Сборщик имеет следующую файловую структуру:

```
├── gulpfile.js         # gulpfile сборщика
├── projectConfig.js    # Конфигурационный файл
└── gulpy/              # Папка с тасками и хелперами для gulp
    └── helpers/        # Хелперы
    └── tasks/          # Основные таски (разложены по папкам в соответствии с типом таска)
    └── user-tasks/     # Пользовательские таски
└── markup/             # Основная папка с проектом
    └── modules/        # Папка с модулями
    └── pages/          # Папка с шаблонами страниц
    └── static/         # Папка для различной статики (css, js и т.п.)
└── docs/               # Документация
```


Структура отдельного модуля
---------------------------

Модуль — самостоятельная единица на странице. Пример модуля — header. Каждая страница состоит из модулей. Любой модуль может включать в себя другие модули.

```
exampleModule/                  # Пример модуля
    └── assets/                 # Различные доп. файлы, относящиейся только к данному модулю
    └── ie/                     # Здесь размещаются стили для ie8 и ie9.
    └── mData/                  # Папка для хранения данных для модуля
        ├── mData.js            # Данные для модуля в виде js-объекта (формат объекта есть в модуле-примере _template)
    ├── exampleModule.html      # Html-представления модуля (также может иметь расширение jade, в зависимости от выборанного шаблонизатора)
    ├── exampleModule.scss      # Scss-представление модуля (less|styl, в зависимости от выбранного css-препроцессора)
    ├── exampleModule.js        # Js-представление модуля

```

Основная идея в том, чтобы сделать модуль абсолютно изолированной структурой. Здесь можно использовать <a href="https://ru.bem.info/" target="_blank">BEM</a>,  <a href="http://webcomponents.org/" target="_blank">веб-компоненты</a> (и их <a href="https://www.polymer-project.org/" target="_blank">реализация от Google</a>), что-то еще. Можно все делать и по старинке, внутри одного модуля вся верстка, но это крайне не рекомендуется.

В `pages` находятся шаблоны страниц, в которые в итоге будут включены модули. Страницы являются лэйаутом и должны содеражть в себе как можно меньше кода, чтобы структура была как можно более прозрачная.
Чтобы создать новую страницу, просто скопируйте существующую (или _template) и переименуйте.

Структура папки для статики
---------------------------

```
static/                                     # Папка для статики. Название для папки настраивается в projectConfig.js
    └── fonts/                              # Папка для шрифтов (может содержать поддиректории)
    └── img/                                # Папка для картинок. Название для папки настраивается в projectConfig.js
        └── content/                        # Папка для контентных картинок (может содержать поддиректории)
        └── plugins/                        # Папка для картинок плагинов (может содержать поддиректории)
        └── general/                        # Папка с общими картинками для проекта (может содержать поддиректории)
        └── sprite/                         # Папка для растровых картинок, которые должны быть включены в спрайт 
            └── 96dpi/                      # Картинки для экранов с dpi 96
            ...
            └── 288dpi/                     # Картинки для экранов с dpi 288 (более подробно <a href="https://github.com/artem-malko/tars/blob/master/docs/images.md">тут</a>)
        └── svg/                            # SVG-картинки
    └── js/                                 # Папка для js
        └── libraries/                      # Папка для js-библиотек (например, jquery)
        └── plugins/                        # Папка для js-плагинов
        └── separateJs/                     # Папка для js-файлов, которые не должны попасть в итоговый склеенный js-файл.
    └── misc/                               # Общие файлы, которые будут перемещены в корень собранного проекта — фавиконка, robots.txt и т.д.  (может содержать поддиректории)
    └── scss|less|stylus/                   
        └── etc/                            # Стили, которые будут подключаться в самом конце (может содержать поддиректории)
        └── plugins/                        # Стили для плагинов (может содержать поддиректории)
        └── spriteGeneratorTemplates/       # Шаблоны, по которым генерируются спрайты
        └── spritesScss|Less|Stylus/        # Миксины для спрайтов  
        ├── common.scss|less|styl           # Общие стили для всего проекта
        ├── fonts.scss|less|styl            # Стили для подключенный шрифтов
        ├── GUI.scss|less|styl              # Стили для GUI-элементов типа кнопок, полей ввода и т.д.
        ├── mixins.scss|less|styl           # Набор миксинов
        ├── normalize.scss|less|styl        # Сброс стилей
        ├── vars.scss|less|styl             # Переменные проекта
```

Структура готовой сборки
-------------------------