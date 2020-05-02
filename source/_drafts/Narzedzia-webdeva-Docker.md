title: 'Narzędzia webdevelopera: Docker'
author: Adam Dziendziel
tags:
  - Toolbox
  - Docker
  - Wordpress
  - Drupal
categories:
  - Tech
date: 2018-06-28 11:58:00
---
Jest to krótki praktyczny wstęp do tego jak używać Dockera i dlaczego w ogóle warto to robić.

## Zastosowanie
W codziennej pracy docker ma dwa podstawowe zastosowania:
### Porządek w systemie
Możemy instalować różne serwery, biblioteki, narzędzia nie bezpośrednio w naszym systemie operacyjnym a w wydzielonym kontenerze.   
Dzięki temu nie musimy się martwić tym, że jeden projekt wymaga PHP 7.0, inny 7.1, nie musimy obok siebie instalować MySQL i Postgres.
To jest szczególnie fajne, gdy jesteś frontendowcem i nagle musisz odpalić jakiś backend napisany w PHP.   
Zamiast instalować MySQL, PHP i Apache w systemie to pobierasz po prostu obraz 
W trochę 

### Uniknięcie problemu "U mnie działa"
Ponieważ możemy zdefiniować środowisko developerskie raz i używać go w identycznej postaci na każdym komputerze członka zespołu.


## Mój przyjaciel docker-compose

Łączenie kontenerów ze sobą może być skomplikowane i nużące, ponieważ

## Użycie dockera
1. `docker-compose build`
2. `docker-compose up`

## Przykład użycia: Wordpress
## Przykład użycia: Drupal


## Więcej informacji
https://www.youtube.com/watch?v=T25Z4CUwYjE&t=626s
