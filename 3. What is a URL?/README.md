# Что находится в URL-адресе?

URL-адреса есть повсюду. Мы используем их для доступа к веб-сайтам, отправки электронных писем, загрузки файлов и многого другого. Но что такое URL-адрес и как он работает? В этой статье мы рассмотрим анатомию URL-адреса, различные типы URL-адресов, способы кодирования и декодирования URL-адресов, способы проектирования и отладки URL-адресов, а также некоторые советы по безопасности при использовании URL-адресов.

- [Что такое URL-адрес?](#что-такое-url-адрес)
- [Анатомия URL-адреса](#анатомия-url-адреса)
- [URL-кодирование](#url-кодирование)
- [Относительные и абсолютные URL-адреса](#относительные-и-абсолютные-url-адреса)
- [URL-маршрутизация](#url-маршрутизация)
- [Лучшие практики по дизайну URL-адресов](#лучшие-практики-по-дизайну-url-адресов)

## Что такое URL-адрес?

*URL-адрес (унифицированный указатель ресурса) - это строка символов, идентифицирующая ресурс в Интернете.*

Ресурсом может быть что угодно, к чему можно получить доступ в Интернете, например, веб-страница, изображение, видео, документ и т.д.

URL-адрес состоит из двух частей: схемы и пути. Схема определяет протокол или метод доступа к ресурсу, например, http, https, ftp, mailto и т.д. Путь указывает местоположение или адрес ресурса на сервере или в сети. Например, вот URL-адрес, состоящий из этих двух частей.

```
https://www.example.com/index.html
--^--   ---------^----------------
scheme          path
```

## Анатомия URL-адреса

URL-адрес может иметь несколько компонентов, которые представляют дополнительную информацию о ресурсе или о том, как получить к нему доступ. Эти компоненты разделяются специальными символами, называемыми разделителями. Базовая структура URL-адреса представлена ниже:

``scheme://[user:password@]host[:port]/path[?query][#fragment]``

- После схемы следует двоеточие **`:`** и две косые черты **`//`**.
- Пользователь и пароль не являются обязательными и используются для целей аутентификации. Они разделяются двоеточием **`:`**, за которым следует знак **`@`**.
- Хост - это имя или IP-адрес сервера или сети, в которой расположен ресурс. Он также может включать субдомен или доменное имя.
- Порт является необязательным и указывает номер порта на сервере, где можно получить доступ к ресурсу. Ему предшествует двоеточие.
- Путь - это последовательность каталогов и файлов, ведущих к ресурсу на сервере. Он отделяется косой чертой **`/`**.
- Запрос не является обязательным и содержит дополнительные параметры или данные, которые отправляются на сервер вместе с запросом ресурса. Ему предшествует вопросительный знак **`?`**.
- Фрагмент не является обязательным и идентифицирует конкретную часть или раздел ресурса. Ему предшествует знак решетки **`#`**.

Вот пример URL-адреса со всеми этими компонентами:

```
https://www.example.com:8080/blog/post.php?id=123&lang=en#comments

- scheme: https
- user: none
- password: none
- host: www.example.com
- port: 8080
- path: /blog/path.php
- query: id=123&lang=en
- fragment: comments
```

## URL-кодирование

Иногда нам необходимо включать в URL-адреса специальные символы или пробелы, которые не разрешены или имеют другое значение в синтаксисе URL-адресов. Например, мы может захотеть выполнить поиск "Программирование на C#" в Google, но мы не можем использовать знак # в нашем запросе, поскольку он используется в качестве разделителя фрагментов. Чтобы решить эту проблему, мы можем использовать кодирование URL или процентное кодирование. Этот процесс преобразования этих символов в формат, которые можно безопасно передать в URL-адресе. Формат состоит из знака **`%`**, за которым следуют две шестнадцатеричные цифры, представляющие код ASCII символа. Например, **`#`** знак кодируется как **`%23`**, а пробел кодируется как **`%20`**. Итак, наш поисковый запрос будет выглядеть так:

``https://www.google.com/search?q=C%23+programming``

Кодирование URL-адреса также можно использовать для кодирования символов, отличных от ASCII, такие как китайские или арабские символы, в формат UTF-8.

## Относительные и абсолютные URL-адреса

Абсолютный URL-адрес - это полный URL-адрес, в котором указаны все компоненты местоположения ресурса, такие как схема, хост, порт, путь, запрос и фрагмент, например:

``https://www.example.com/blog/post.php?id=123&lang=en#comments``

Относительный URL-адрес - это неполный URL-адрес, в котором отсутствуют некоторые или все эти компоненты, и для их разрешения используется контекст или базовый URL-адрес, например:

``/blog/post.php?id=123&lang=en#comments``

Этот относительный URL-адрес можно преобразовать в абсолютный URL-адрес, если мы знаем, что он относится к тому же хосту и схеме, что и базовый URL-адрес:

``https://www.example.com/blog/post.php?id=123&lang=en#comments``

Это полезно, когда мы хотим создать ссылку на ресурс на том же веб-сайте или сервере. Например, мы можем использовать относительный URL-адрес для ссылки на другую страницу на том же веб-сайте:

``<a href="/about">About</a>``

## URL-маршрутизация

Маршрутизация URL-адресов - это процесс определения того, какой ресурс обслуживать, на основе URL-адреса запроса. Различные веб-серверы и платформы имеют разные способы реализации маршрутизации URL-адресов, но основная идея состоит в том, чтобы сопоставить URL-адрес с предопределенным шаблоном или правилом, определяющим, какой ресурс обслуживать. Например, простое правило может быть таким:
- Если URL-адрес **`/home`**, укажите домашнюю страницу.
- Если URL-адрес **`/blog/post?title=whats-in-a-url`**, разместите сообщение в блоге с заголовком "Что находится в URL-адресе?".
- Если URL-адрес **`/about`**, откройте страницу с информацией
- Если URL-адрес не соотвутствует ни одному из этих правил, отобразите страницу **`404`** (не найдена).

Маршрутизация URL-адресов также может включать извлечение параметров из URL-адреса и передачу их ресурсу. Например, в URL-адресе **`/blog/post?title=whats-in-a-url`** заголовок параметра имеет значение **`what-in-a-url`**. Это значение может использоваться ресурсом записи блога для отображения соответствующего контента.

Маршрутизация URL-адресов может быть статической или динамической. Статическая маршрутизация означает, что правила фиксированы и не меняются в зависимости от запроса. Динамическая маршрутизация означает, что правила гибкие и могут меняться в зависимости от запроса. Например, правило динамической маршрутизации может быть таким:
- Если URL-адрес **`/blog/post/<slug>`**, поместите сообщение в блоге со слагом **`<slug>`**.
- Если сообщение в блоге с таким ярлыком не существует, отправьте страницу 404.

В данном случае **`<slug>`** это переменная, которая может принимать любое значение. Например, **`/blog/post/whats-in-a-url`** и **`/blog/post/how-to-design-urls`** оба являются допустимыми URL-адресами, соответствующими этому правилу.

## Лучшие практики по дизайну URL-адресов

Дизайн URL-адресов - важный аспект веб-разработки, который влияет на удобство использования, поисковую оптимизацию (SEO) и удобство обслуживания. Вот несколько рекомендаций по созданию ясных, последовательных и содержательных URL-адресов:
- Используйте описательные слова вместо цифр или кодов. Например, **`/blog/post/funny-cats`** лучше, чем **`/blog/post/12345`**.
- Для разделения слов используйте дефисы (**`-`**) вместо подчеркиваний (**_**) или пробелов (**`%20`**). Например, **`/blog/post/whats-in-a-url`** лучше, чем **`/blog/post/whats_in_a_url`** или **`/blog/post/whats%20in%20a%20url`**.
- Используйте строчные буквы вместо заглавных.
- Используйте короткие и простые URL-адреса вместо длинных и сложных.
- Избегайте использования ненужных слов и символов в URL-адресах.
- Используйте в URL-адресах ключевые слова, которые имеют отношение к вашему контенту или целевой аудитории.
- Будьте последовательны в структуре URL-адресов и соглашениях на своем веб-сайте.
- Не меняйте URL-адреса после их публикации. Если вам нужно изменить URL-адрес, используйте перенаправление, чтобы перенаправить запросы со старого URL-адреса на новый URL-адрес.
- Используйте канонические URL-адреса. Канонические URL-адреса - это предпочтительные версии ваших страниц, которые вы хотите, чтобы поисковые системы индексировали и отображали. Вам следует использовать канонические теги или перенаправления, чтобы избежать проблем с дублированием контента, вызванных различиями в ваших URL-адресах. Например, если у вас есть несколько URL-адресов, указывающих на одну и ту же страницу, вам следует указать один из них в качестве канонического URL-адреса и перенаправлять или ссылаться на него с других.