<!--
title: PUSHTOKEN
description: 
published: true
date: 2023-11-21T13:20:43.182Z
tags: 
editor: ckeditor
dateCreated: 2023-09-08T07:12:40.361Z
-->

# **PUSHTOKEN – запрос на передачу токена КПК (Registration Token)**

Передает идентификационный токен мобильного устройства. Используя токен можно отправлять из 1С на мобильное устройство PUSH уведомления.

```plaintext
<ВерсияПротоколаОбмена>\r\n
<Платформа>\r\n
<КодАгента>\r\n\
PUSHTOKEN\r\n
<РегистрационныйТокенКПК>\r\n
Ответ:
OK\r\n
 
```

> Используется в функции [Уведомления](/integraciya-s-1s-8-ut-10/agenty/uvedomleniya)