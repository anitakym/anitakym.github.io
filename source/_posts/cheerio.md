---
title: cheerio
date: 2019-11-29 17:50:11
tags:
    - node
    - jQuery
---

#### Cheerio
官方文档指路：https://github.com/cheeriojs/cheerio/wiki/Chinese-README

Fast, flexible, and lean implementation of core jQuery designed specifically for the server.

极其灵活：cheerio使用了@FB55编写的非常兼容的htmlparser2，因此它可以解析几乎所有的HTML和XML


const cheerio = require('cheerio');
const $ = cheerio.load('<ul id="fruits">...</ul>');


const $ = cheerio.load('<ul id="fruits">...</ul>', {
    normalizeWhitespace: true,
    xmlMode: true
});


These parsing options are taken directly from htmlparser2, therefore any options that can be used in htmlparser2 are valid in cheerio as well. The default options are:
{
    withDomLvl1: true,
    normalizeWhitespace: false,
    xmlMode: false,
    decodeEntities: true
}


#### htmlparser2
Forgiving html and xml parser
