# MegaCRM Печать термоэтикеток в формате Xprint

Этот проект позволяет автоматизировать процесс печати термоэтикеток в формате Xprint через MegaCRM. На этикетке печатается артикул, наименование товара и линейный штрих-код в количестве, указанном в сделке.

## Описание

Печать термоэтикеток помогает автоматизировать процессы учёта и управления товарами, что значительно упрощает работу с большим количеством продукции. В данном проекте используется HTML-шаблон, который можно вставить в MegaCRM для генерации этикеток.

## Использование

1. Скопируйте предоставленный HTML-код.
2. Создайте новый документ в MegaCRM.
3. Вставьте скопированный код в шаблон документа в режиме HTML.
4. Настройте размеры термоэтикетки, изменив параметры `width` и `height` в CSS.

HTML-код для вставки в MegaCRM:
```markdown
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
```markdown
## Редактирование размера термоэтикетки

Для изменения размера термоэтикетки отредактируйте следующие параметры в CSS:
```html
    width: 58mm;
    height: 40mm;
```markdown
## Лицензия

Этот проект распространяется под лицензией MIT. Подробности см. в файле [LICENSE](LICENSE).

