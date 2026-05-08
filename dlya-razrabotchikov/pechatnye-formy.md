<!--
title: Печатные формы
description: 
published: true
date: 2024-07-29T13:47:40.647Z
tags: 
editor: ckeditor
dateCreated: 2023-09-08T07:15:19.860Z
-->

Печатная форма это обычный, текстовый файл в формате xml. Файлы печатных форм хранятся в основном каталоге Моби-С в папке **Forms**.

Содержимое файла может быть произвольным, поэтому не возможно предоставить инструкцию по созданию печатной формы. Обычно берется за основу файл какой-то имеющейся печатной формы и изменяется.

Печатные формы загружаются на КПК в подзапросе **PrnForms** запроса [FullLoad](/dlya-razrabotchikov/format-obmena-dannyh/FullLoad). В данном запросе передается название печатной формы, объект для которого актуальная печатная форма и текст формы. [Настройка печатных форм на КПК](/integraciya-s-1s-8-ut-10/servis/nastrojka-pechatnyh-form-na-kpk)

Данные в печатной форме передаются через переменные ([Список доступных переменных)](https://drive.google.com/open?id=1A-f2u2f5SfUwsR_iMT40Da18IEu7iDR9LDSlce8_LjQ)

...

В печатных формах можно использовать значения [дополнительных реквизитов](/dlya-razrabotchikov/dopolnitelnye-rekvizity). Для этого нужно использовать параметр **Req\_КодРеквизита**.

## **Добавление изображения на печатную форму**

Все используемые параметры и типы описаны выше в документации. Это базовые примеры для быстрой вставки основных типов изображений.

### **Встраивание изображения в печатную форму**

Необходима конвертация файла картинки в формат Base64. Сделать это можно на сайте [https://www.base64encode.org](https://www.base64encode.org/). Полученный текст вставьте в пример, вместо жирного текста.

![](/smile.png)

<Cell Image="data:image/png;base64,**iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz AAALEwAACxMBAJqcGAAAAiJJREFUOI2Nks9LVFEUxz/nvDfjNGYZEi4szShLKppkqAQpkgQjF5VY ixZBC120cWjh/xCBlCQ2u6CdhhC2MEjCRUgoRUS0KBGKosCM0l44vnNbvHHSUcQDl3PPvef7PT+F IrF3Fxucr10414xPDQKIziA2pr43ILsGX6/0l+WLm2xLWiLRp8p1BND8b5E2dVlBurV6KCgQuMm2 pGl8VH1t2ghcIBHGRWnV6qFAAYxEnzptIoTNHDVOudB6AcReXG4Qz02hjrvDP1BPOJ1KcmRfyZro oxMLqActjaXRu8oxdRZ2YUAoNB0u5fe8kX08F0UzVulM7zcyt78XbFuyTh+jGaIIwR8jc6mCREke 5PIZ5PWd7krUk4hUAXHNEo61L6qvsfWb5jZuptqiTxgZA6Nz3BqeLV6LdaXnagVdF8qjhoLOEEJ9 VcmmwACHauL5Pui0T8gYyv6muiS7K2J8ms3RoeXsJLYK9JUcw/aTmsoYjfVJ8pk/EzfSkcLjFQoT HwKu3fvClB5E/y8pADkcJ9x7HvZUkT6QAHU4dUcFIHzSfl9FO1F4+TFgz0AZW52uIvilIZ8zC6Tr EqBgQr93cvCGAsi8dNuSGyeE47Vb2J5aW/eONKT3JqL5hzzXIHkTooGgV4YCCWi10LIYxFtDZJsr gKUc4udtGdyvueQ5OfPgL1BUKOBGOlJm1mnztIRv/VoEvAab1jL3VNRl9eyjNyv9/wF00c7KoatP MwAAAABJRU5ErkJggg==**" Scale="None" />

## **Добавление на форму штрих-кода с номером документа**

В Моби-С есть возможность добавить в любую печатную форму штрих-код в котором выводиться номер документа. Это может пригодиться при поиске сканированием штрх-кода с формы документа соответствующего документа в 1С.

Для работы со штрих-кодами во всех документах добавлены две переменные и один признак

**Doc.ExtId** - Уникальный идентификатор документа в 1С. На КПК доступен только после выгрузки документа в 1С. В протоколе обмена соответствует реквизиту **СсылкаНаДокумент**.

Пример: <Cell Text="Doc.ExtId" LabelType="Expression" Barcode="Code128B"/>

**Doc.NumberBarcode** \- Внутренний номер документа на КПК(КодДок) или номер документа полученного из 1С(НомерДокумента). Если документ не выгружен то выводиться **КодДок**, если выгружен то **НомерДокумента**. Данные выводятся конвертированные в формат **Base64**.

Пример: <Cell Text="Doc.NumberBarcode" LabelType="Expression" Barcode="Code128B"/>

**BarCode** - выводить текст в виде штрих-кода.

[Варианты нумерации в Моби-С](/dlya-razrabotchikov/numeraciya-dokumentov) Пока документ не выгружен на КПК есть только внутренний код документа. В случае если используется нумерация **Номер присваивает 1С** на КПК нет ни какой возможности вывести в штрих код правильный номер документа. Если вы планируете выводить штрих код то мы рекомендуем использовать две оставшиеся схемы нумерации документов.

Мы рекомендуем использовать такой код: <Cell Text="CASE WHEN Doc.ExtId = '' THEN Doc.NumberBarCode ELSE Doc.ExtId END" LabelType="Expression" Barcode="Code128B"/>

Если документ уже выгружен то в штрих-код выводиться уникальный идентификатор документа из 1С, если не выгружен то внутренний номер документа на КПК.