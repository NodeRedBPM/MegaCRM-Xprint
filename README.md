# MegaCRM Печать термоэтикеток в формате Xprinter

![MegaCRM Печать термоэтикеток в формате Xprint](https://github.com/NodeRedBPM/MegaCRM-Xprint/blob/main/xprint.jpg)

Этот проект позволяет автоматизировать процесс генерации штрих-кодов артикула товара и печати термоэтикеток в формате Xprint, при использовании MegaCRM. На этикетке печатается артикул, наименование товара и линейный штрих-код. 
Количество выводимых на печать термоэтикеток, соответствует сумме количеств каждой позиции товара в соответствии со списком товаров указанных в сделке.

## Описание

Печать термоэтикеток помогает автоматизировать процессы учёта и управления товарами, что значительно упрощает работу с большим количеством продукции. В данном проекте используется HTML-шаблон, который можно вставить в MegaCRM для генерации штрих кодов и печати этикеток.

## Использование

1. Скопируйте предоставленный HTML-код.
2. Создайте новый документ в MegaCRM.
3. Вставьте скопированный код в шаблон документа в режиме HTML.
4. Настройте размеры термоэтикетки, изменив параметры `width` и `height` в CSS.
   
![MegaCRM Печать термоэтикеток в формате Xprint](https://github.com/NodeRedBPM/MegaCRM-Xprint/blob/main/megacrmxprint.png)

HTML-код для создания шаблона нового документа в MegaCRM:
```html
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <style type="text/css">
        @media print {
            @page {
                size: 58mm 40mm; /* Размер этикетки */
                margin: 0;
            }
            body {
                margin: 0;
                padding: 0;
                width: 58mm;
                height: 40mm;
                font-family: Arial, sans-serif;
                font-size: 10px;
                line-height: 1.2;
            }
            .container {
                width: 58mm;
                height: 40mm;
                border: 0;
                display: flex;
                flex-direction: column;
                justify-content: center;
                font-size: 10px; /* Уменьшенный шрифт */
                line-height: 1.2;
                align-items: center;
                padding: 5mm; /* Отступы, если необходимо */
            }
            .barcode {
                margin-top: 5mm; /* Отступ для штрих-кода */
            }
        }
    </style>

    {foreach from=$deal.products item=product}
        {for $i=1 to $product.amount}
            <div class="container">
                <div>
                    <p>{$product.name}</p>
                </div>
                <img alt="Штрих-код" class="barcode" src="https://barcode.tec-it.com/barcode.ashx?data={$product.article}&amp;code=Code128&amp;dpi=96" />
            </div>
            <div style="page-break-after: always;">&nbsp;</div>
            <!-- Разрыв страницы -->
        {/for}
    {/foreach}
```
## Редактирование размера термоэтикетки

Для изменения размера термоэтикетки отредактируйте следующие параметры в CSS:
```html
size: 58mm 40mm; /* Размер этикетки */

    width: 58mm;
    height: 40mm;
```
### Генерация штрих-кодов или QR-кодов

Генерация штрих-кодов в данном проекте производится через бесплатный API сервис **https://barcode.tec-it.com**. С помощью этого сервиса Вы сможете сгенерировать такие штрихкоды, как EAN, UPC, GS1 DataBar, Code-128, QR Code®, Data Matrix, PDF417 и.т.д.
При необходимости, замените этот сервис на другого поставщика штрих-кодов. Для этого измените URL в теге `<img>`, где указан источник изображения штрих-кода.

Используемый в коде пример использования API для генерации линейного штрих кода:
```html
<img alt="Штрих-код" class="barcode" src="https://barcode.tec-it.com/barcode.ashx?data={$product.article}&amp;code=Code128&amp;dpi=96" />
```
Пример для генерации QR-кода вместо линейного штрих кода:
```html
<img alt="QR-код" class="barcode" src="https://barcode.tec-it.com/barcode.ashx?data={$product.article}&amp;code=QRCode&amp;dpi=96" />
```
## Лицензия

Этот проект распространяется под лицензией MIT. Подробности см. в файле [LICENSE](LICENSE).

