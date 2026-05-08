<!--
title: CurrentPosition
description: 
published: true
date: 2023-11-10T13:03:33.022Z
tags: 
editor: ckeditor
dateCreated: 2023-09-08T07:09:57.725Z
-->

# **CurrentPosition – запрос на выгрузку последних GPS координат агентов**

```plaintext
<ВерсияПротоколаОбмена>\r\n
\r\n
CurrentPosition\r\n
[<КодАгента>\t<ДатаВремя>\t<Долгота>\t<Широта>\t<Скорость>\r\n]
```

Список последних координат торговых агентов. Скорость предается в км/час.