# DigiTest

JavaScript
#1. 
Каким будет результат следующей операции на языке JavaScript: [1, 2, 3] + [4, 5, 6]. Почему был получен такой результат?

#Ответ: При сложении массивы будут преобразованы в строки, поэтому результат: “1, 2, 34, 5, 6”
#2. 
Дано выражение:
var a = {b: 1};
var b = a;
b.b = 2;
console.log(a);
Что будет выведено в консоли? Почему был получен такой результат?
#Ответ: Результат: {b: 2}. Переменные a и b относятся к одному объекту, поэтому при изменении объекта в одной переменной, он обновляется и во второй.
#3. 
Написать регулярное выражение, совпадающее с числом с плавающей точкой с точностью до 3 знака после запятой.
#Ответ: ^-?\d+(\.\d{1,3})?$
#4. 
Написать регулярное выражение, по которому определяется является ли строка ссылкой. Объяснить, как оно работает.
Пример:
const isURL = str => true
isURL(‘https://example.com’)
isURL(‘http://www.example.com’)

#Ответ: ^(https?:\/\/)?([\da-z.-]+)\.([a-z.]{2,6})([\/\w .-]*)*\/?$
(https?:\/\/)? - необязательная часть ссылки (http:// или https://)
([\da-z.-]+) - доменное имя
\.([a-z.]{2,6}) - доменная зона (.com)
([\/\w .-]*)*\/? - т.к. после домена может идти еще какой-либо путь, то необходима проверка на это (http://www.example.com/test). Эта часть также необязательна.
#5.
Каким будет значение переменной text после выполнения данного JavaScript кода? 
function setText(message) { 
text = message;
 }
 var text = 'Текст';
 setText('Сообщение');
Опишите, почему получился такой результат.
#Ответ: Значение будет 'Сообщение', так как, используя Var при создании переменной, она инициализируется глобально, поэтому при изменении переменной в функции, её значение изменяется.

6.
Написать функцию для получения список всех артикулов товаров в консоли браузера на странице https://groupprice.ru/categories/jenskaya-odejda?referer_from=main_catalog
Ответ:
``` js
function getAllProductArticles() {
    const products = document.querySelectorAll('.__products--list ._product');
    const articleList = [];
    products.forEach(element => {
        articleList.push(element.attributes[1].nodeValue);
    });
    return articleList;
}

console.log(getAllProductArticles());
```

7. 
Написать функцию для получения всех характеристики товара в консоли браузера в виде объекта в формате attributeName: value на странице https://nir-vanna.ru/product/smesitel-bravat-art-f175109c-dlya-rakoviny/
Ответ:
``` js
function getAllProductCharacteristics() {
    const productParameters = document.querySelectorAll('.tab-pane-product-parameters-main .tab-pane-product-parameter-item');
    const characteristicsList = [];
    productParameters.forEach(element => {
        characteristicsList.push({[element.children[0].innerText.trim().split("\n")[0]]: element.children[1].innerText});
    });
    return characteristicsList;
}

console.log(getAllProductCharacteristics());
```
