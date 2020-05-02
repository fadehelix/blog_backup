title: Sprawdzanie aktualizacji bibliotek npm
author: Adam Dziendziel
tags: []
categories: []
date: 2017-06-29 20:09:00
---
Jakiś czas temu opisałem moje przygody z aktualizowaniem zależności w projekcie. Wtedy skupiłem się na SemVer i tym jak . Dzisiaj rozwijam ten temat

## Taczki
Najpierw opiszę narzędzie lekkie, proste i szybkie w użyciu nie zawierające żadnej magicznej automatyzacji.

Jest nim komenda `$ npm-check`, a wynik jej użycia na jednym z moich projektów wygląda następująco:
![Przykład użycia komendy npm-check](/images/npm-aktualizacja-npm-check.png)





## Koparka
Jeśli pracujemy w zespole przy większym projekcie (albo open source) to stać nas na poświęcenie parunastu minut na skonfigurowanie narzędzia sprawdzającego zależności na poziomie repozytorium
[Greenkeeper](https://greenkeeper.io/)
* Działa z Github
* Darmowy dla projektów opensource
* Automatycznie sprawdza nowsze wersje zależności
* Tworzy osobny branch na którym robi 'npm install' oraz 'npm test'

Jedną z alternatyw jakie znalazłem jest [Gemnasium](https://gemnasium.com/). Na początku myślałem, że to taki Greenkeeper dla Ruby (bo nazwa), ale szybko zobaczyłem, że ta usługa sprawdza zależności dla npm, yarn php (packagist), python (pypi) i oczywiście ruby (gemy).