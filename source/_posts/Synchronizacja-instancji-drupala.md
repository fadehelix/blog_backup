title: Synchronizacja instancji drupala
author: Adam Dziendziel
tags:
  - drupal
  - drush
categories:
  - Tech
date: 2018-03-20 18:27:00
---
![](/images/drupal-synchronizacja-intro.jpeg)

## Przenoszenie zmian pomiędzy instancjami strony.
Nawet jeśli pracujesz nad stroną sam, chcesz mieć możliwość łatwego przenoszenia kodu oraz treści chociażby z twojego lokalnego środowiska developerskiego na serwer.   
W najprostszej standardowej konfguracji workflow może być złożone z klienta FTP oraz klienta bazy MySQL takiego jak [MySQL Workbench](https://www.mysql.com/products/workbench/) (nie jesteśmy uzależnieni od tego, czy nasz hosting pozwala nam używać PhpMyAdmin).   
No i to w zasadzie pozwala nam przenosić kod strony oraz bazę danych w obie strony bez ogromnego nakładu pracy.

Zaleta jest taka, że są to uniwersalne narzędzia i sposób działający zarówno przy pracy z Drupalem, Wordpressem czy nawet czystym Symfony, jednak Drupal oferuje nam ciekawsze, dające więcej możliwości i kosztujące mniej pracy zabawki.


## Rozwiązanie 1: Klikanie
__Poziom trudności:__ Łatwy   
__Wymagania:__ Moduł [Backup and Migrate](https://www.drupal.org/project/backup_migrate).

Po włączeniu modułu wchodzimy na `/admin/config/development/backup_migrate` i wybieramy backup czego chcemy zrobić (tylko baza danych? A może pliki? A co tam, całą stronę od razu też można "zbekapować"!)

Aby wprowadzić zmiany na innej instancji strony wchodzimy na `/admin/config/development/backup_migrate/restore` i wybieramy dokładnie tą opcję co w kroku poprzednim (musi być ta sama, czyli jeśli zrobiliśmy kopię bazy danych to tutaj też wybieramy opcję "baza danych")

Profit <3


## Rozwiązanie 2: Drush
__Poziom trudności:__ Średni   
__Wymagania:__ Dostęp do konsoli oraz zainstalowany [drush](http://www.drush.org/)    

A myślałem, że będzie tak pięknie... po tylu latach pracy z Drupalem drush stał się moim podstawowym narzędziem, używam go w zasadzie podświadomie nawet do chyba najpopopularniejszej czynności związanej z developmentem, czyli czyszczeniem pamięci podręcznej (`drush cr all`).   

Bardzo przydatną rzeczą, którą daje nam drush są aliasy instancji stron. Dzięki nim możemy, bedąc w katalogu projektu na swoim komputerze, uruchomić drusha na serwerze bez konieczności pamiętania danych dostępowych, bo wszystko zawieramy raz w konfiguracji aliasu.   
Chcąc skopiować lokalną bazę danych na serwer wystarczy, że użyjemy takiej komendy:   
```
drush sql-sync @local @dev
```

Gdzie __@local__ oraz __@dev__ to zdefiniowane w pliku `~/.drush/aliases.bashrc.php` moje instancje drupala.   
Na blogu Acquia znajduje się [bardzo fajny tutorial](https://dev.acquia.com/blog/use-drush-to-sync-your-drupal-installations-between-multiple-environments/06/04/2016/10236).   
Super, do dzieła!

### Lecz nadszedł Drupal 8.4 i Drush 9
Co w moim przypadku wyglądało jak zderzenie się z ekipą olimpijską w bokserskiej wadze średniej:   
Lewy sierpowy: Okazało się, że Drush 8 nie działa z wersją 8.4 Drupala.   
Prawy podbródkowy: Jedynym sposobem instalacji najnowszej wersji Drush jest `composer require drush/drush`   
Lewy prost: Zmieniły się komendy (a konkretnie ich zapis)
Prawy sierp: Nie działają wszystkie wcześniejsze "commandfiles", czyli np. *.drush.inc, aliases.drushrc.php...   
Nokaut. Lężę. Jęczę. Widzę na monitorze latające gwiazdki.

![Zgodność Drush z wersjami Drupala](/images/drupal-synchronizacja-tabela-drush.png)

W Drush 9 zaszło sporo zmian na poziomie architektury, ale dla mnie teraz najważniesze są takie, że:
- drusha instaluje się composerem lokalnie w projekcie
- konfiguracja aliasów odywa się w plikach .yml
- aliasy są trzymane w projekcie, a nie globalnie ( u mnie jest to katalog `drush/sites`)

Aby zobaczyć jak w nowy sposób zdefiniować aliasy najlepiej [zobaczyć przykład](https://github.com/drush-ops/drush/blob/master/examples/example.site.yml).

Teraz pozostaje nam już tylko zrobić sync po nowemu:
```
drush sql:sync @local @dev
```