# ШРИ: Тулинг 2023 часть 2

## Общий комментарий

- Объем исходных данных на сайте составляет около 15 МБ, из которых около 5 МБ передано по сети. Сжатие данных
  произведено довольно хорошо. Общее время загрузки (Load) составило 2 секунды.

![network tab](./img/0img.png "network tab")

## 1 Tab network Google Chrome

### 1.1 [HAR файл](./www.gd.ru.har)

#### 1.2 Неоптимальные места

##### 1.2.1. Дублирование ресурсов. Можно заметить случаи, когда некоторые запросы к одним и тем же ресурсам происходят несколько раз без видимой причины.

Например:
![network tab](./img/1double.png "network google chrome")
Есть и другие примеры, но они не такие явные. Например, вот такой запрос:

- www.1cont.ru
- fontawesome-webfont.woff2

##### 1.2.2. Лишний размер ресурса

- Элементы графики используют растовые изображения, хотя могли бы использовать векторные.
![network tab](./img/2img.png "network tab")

- Большой размер JS и CSS файлов.
- 
![network tab](./img/3img.png "network tab")

##### 1.2.3. Медленно загружающиеся ресурсы
- Неоптимальное использование сторонних библиотек (например, jquery, которая весит 85kb, и bootstrap, которая весит более 250kb.
![network tab](./img/5img.png "network tab")
![network tab](./img/4img.png "network tab")

- часть запросов завершается ошибкой:

![network tab](./img/6img.png "network tab")
##### 1.2.4. Ресурсы, блокирующие загрузку
- Ресурсы, которые запускаются до того, как страница полностью загрузится. Например, вот такие запросы:
![network tab](./img/7img.png "network tab")


### 2. На вкладке Perfomance Google Chrome

#### 2.1. Профиль загрузки страницы [Performance JSON](./Trace-Perf.json)

#### 2.2. Измерение времени в миллисекундах от начала навигации до событий First Paint (FP), First Contentful Paint (FCP), Largest Contentful Paint (LCP), DOM Content Loaded (DCL), Load
![8img.png](img/8img.png)

- First Paint (FP) - 726.9 ms

![fp_img.png](img%2Ffp_img.png)

- First Contentful Paint (FCP) - 726.9 ms

![fcp_img.png](img%2Ffcp_img.png)

- Largest Contentful Paint (LCP) - 726.9 ms

![lcp_img.png](img%2Flcp_img.png)

- DOM Content Loaded (DCL) - 1047.7 ms

![dcl_img.png](img%2Fdcl_img.png)


- Load - 2140.9 ms

![Load_img.png](img%2FLoad_img.png)

#### 2.3. DOM-элемент на котором происходит LCP

- `<img loading="lazy" src="/images/branding/10/imageTop_1628667062.7856.jpg" data-url="/images/branding/10/imageTop_1628667062.7856.jpg" alt="-">`

![14img.png](img%2F14img.png)

#### 2.4. Время в ms тратится на разные этапы обработки документа (Loading, Scripting, Rendering, Painting)

- Loading - 39 ms
- Scripting - 2587 ms
- Rendering - 440 ms
- Painting - 325 ms

![10img.png](img%2F10img.png)


### 3. На вкладке Coverage

#### 3.1. Профиль загрузки страницы 

![11img.png](img%2F11img.png)


#### 3.2. Объём неиспользованного CSS в ходе загрузки страницы
- более 500 кб
- 
- ![12img.png](img%2F12img.png)

#### 3.3. Объём неиспользованного JS в ходе загрузки страницы

- более 2000 кб
- 
- ![13img.png](img%2F13img.png)
