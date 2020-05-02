title: 'Jest Hotel, jest impreza!'
author: Adam Dziendziel
tags:
  - Tools
  - Node
  - Express
  - Hexo
categories:
  - Tech
date: 2017-06-02 15:00:00
---
![](/images/hotel-intro.jpeg)
## Ale że jaka impreza?
Moja ścieżka frontendowca prowadzi mnie coraz dalej, a im dalej w last tym więcej drzew, projektów znaczy. Takich lokalnych na których testuję i uczę się nowych rzeczy. Z racji tego, że w większości są to projekty oparte o React/Node/Espress to każdy z nich wymaga uruchomienia swojego serwera.    
W dodatku projekty mam w różnych lokalizacjach w zależności od tego, czy to forki "obcych" repozytoriów, czy po prostu lokalny mały projekcik. Albo też duży lokalny projekt, taki co to ma szansę stać się dostępnym publicznie projektem.
Słowem: jedno wielkie kreatywne bunga-bunga.

## I w jakim hotelu?

Ta nazwa to kryptonim pewnego wcale nie tajnego projektu mającego na celu ułatwienie kontroli nad ~~światem~~ lokalnymi serwerami developerskimi (roboczymi? hasztag _polskietlumaczenia_).


I tutaj światła reflektorów padają na dzisiejszego bohatera: Projekt [Hotel](https://github.com/typicode/hotel)!

Jest to menedżer procesów, a konretnie panel pozwalający nam włączać/wyłączać serwery takie jak:   

* Node (Express, Webpack)
* PHP (Laravel, Symfony)
* Ruby (Rails, Sinatra, Jekyll)
* Python (Django)
* Docker
* Go
* Apache, Nginx

Wszystkie informacje wypisywane w konsoli są potem wyświetlane w przeglądarce. Co prawda sam uważam, że jest to mniej czytelne, niż konsola, głównie ze względu na [brak kolorowania tekstu](https://github.com/typicode/hotel/issues/196).


## Poka poka!

### Dodaję serwery
Server mojego bloga działającego na [Hexo](http://hexo.io)
```bash
$ cd /sciezka/do/projektu/
$ hotel add 'hexo server' -p 4000
```

Serwer mojego projektu wykorzystującego React:   
```bash
$ cd /sciezka/do/projektu/
$ hotel add 'npm start'
```
Tutaj port będzie losowy, co jest bardzo użyteczne jeśli pracujemy na kilku projetach używających np. [create-react-app](https://github.com/facebookincubator/create-react-app), czyli mielibyśmy konflikt portów.    
Dzięki Hotel nie musimy o tych portach w ogóle myśleć, bo dostajemy link do naszej aplikacji oraz nazwę hosta __nazwa-projektu.dev__.

## Panel
Zarządzać wszystkim możemy pod adresem [localhost:2000](http://localhost:2000) lub [hotel.dev](http://hotel.dev) jeśli [ustawiliśmy proxy](https://github.com/typicode/hotel/blob/master/docs/README.md).

![Hotel w pełnej krasie](/images/hotel-screen-1.png)

### Genymotion iksde
Chciałem tylko sprawdzić, a zadziałało.    
Otóż żeby uruchomić emulator Genymotion trzeba w konsoli przejść do katalogu narzędzia i uruchomić go komendą `$ ./genymotion`.   
Pomyślałem, że skoro w Hotel mam serwery to fajnie by też było w tym samym miejscu móc uruchamiać inne usługi developerskie. Tak więc w katalogu Genymotion wpisałem `$ hotel add './genymotion`.    
No i się pojawiło w panelu. Mogę teraz włączać emulator z miejsca, gdzie mam też serwer aplikacji używającej React Native.    
Ja to lubię.

## Kropka
To była krótka notka o małym narzędziu, które może, ale wcale nie musi okazać się przydatne komukolwiek. Ja sam jestem bardzo przywiązany do konsoli i na pewno Hotel jej nie zastępuje, ale jest fajną podstawą, aby stworzyć swojego forka i dodać własne rozwiązania. 

Dzięki za wizytę, mam nadzieję, że nie było to stracone kilka minut Twojego życia :)