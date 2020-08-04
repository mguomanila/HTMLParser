HTML parser<br />
===========
This library is a fast parser of html code that can work with invalid code<br/>
At the entry you must submit a document in UTF-8 or DOM Document encoding.<br/>
To search for elements, css selectors are used which are internally converted<br/>
to an xpath expression.
The resulting xpath expression is cached if the second argument was not set <br/>
to false in the get method(you should disable caching only in the case of <br/>
dynamic generation of css expressions).
The arrays returned ->toArray() contain attributes, text under the #text and <br/>
nested elements under numeric keys.

Alternative methods: ->toXml() return HTML string, ->getDOM() return
DOMDocument.

Basic usage<br />
===================================
```php
<?php
$html = gzdecode(file_get_contents('http://habrahabr.ru/'));

$saw = new nokogiri($html);
var_dump($saw->get('a.habracut')->toArray());
var_dump($saw->get('ul.panel-nav-top li.current')->toArray());
var_dump($saw->get('#sidebar dl.air-comment a.topic')->toArray());
var_dump($saw->get('a[rel=bookmark]')->toArray());

foreach ($saw->get('#sidebar a.topic') as $link){
    var_dump($link['#text']);
}
```

HTML errors will be ignored.
Creating from HTML string: `nokogiri::fromHtml($htmlString)` or `new nokogiri($htmlString)`
Creating from DomDocument: `nokogiri::fromDom($dom)`

TОшибки html игнорируются.
Создание из строки HTML: nokogiri::fromHtml($htmlString); или new nokogiri($htmlString);
Создание из DomDocument: nokogiri::fromDom($dom);


Implemented css selectors<br />
=========================
* tag
* .class
* \#id
* \[attr\]
* \[attr=value\]
* :first-child
* :last-child
* :nth-child(a)
* :nth-child(an+b)
* :nth-child(even/odd)


Requirements<br />
============
DOM
libxml
PHP

Links<br />
============
More articles on the links below:

* <a href="http://habrahabr.ru/blogs/php/110112/">Нокогири: парсинг HTML в одну строку</a>
* <a href="http://habrahabr.ru/blogs/php/114323/">Сравнение библиотек для парсинга</a>
