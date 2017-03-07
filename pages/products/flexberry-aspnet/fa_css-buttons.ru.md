---
title: Кнопки на CSS
sidebar: flexberry-aspnet_sidebar
keywords: Flexberry ASP-NET
toc: true
permalink: ru/fa_css-buttons.html

---

* **Продукт**: [Flexberry ASP.NET](fa_flexberry-a-s-p-n-e-t.html)
* **Компонент**: [Решения по верстке страниц и CSS](fa_page-layout.html)
* **Предназначение**: инструкция, как сделать кнопки на CSS.

## Создание CSS-класса для ссылки

```html
<a href="#" class="btn">Кнопка</a>
```
```css
<style>
.btn{
    /* здесь указываются атрибуты CSS */
    display: inline-block;
    padding: 4px 12px;
    font-size: 14px;
    line-height: 20px;
    color: #000;
    cursor: pointer;
    vertical-align: middle;
    background: #FFF;
    border: 1px solid #CCC;
}
</style>
```

## Состояния кнопок

Псевдоклассы определяют динамическое состояние элементов, которое изменяется со временем или с помощью действий пользователя, а также положение в дереве документа.

* обычная
* выделенная (псевдокласс :hover)
* нажатая (псевдокласс :active)

```css
.btn:hover{
    background: #CCC;
    border: 1px solid #AAA;
}

.btn:active{
    background: #777;
    border: 1px solid #999;
}
```

## Откуда ссылаются на эту страницу

* [CSS](gbt_css.html)
* [Решения по верстке страниц и CSS](fa_page-layout.html)


## Куда ссылается эта страница

* [Flexberry ASP.NET](fa_flexberry-a-s-p-n-e-t.html)
* [Решения по верстке страниц и CSS](fa_page-layout.html)