title: 'Genymotion jako alternatywny emulator Android '
author: Adam Dziendziel
tags:
  - ReactNative
  - Android
  - DSP2017
categories:
  - Tech
date: 2017-05-29 11:59:00
---
Pracując przy tworzeniu aplikacji mobilnej niezwykle użyteczny jest emulator smartfona. W sensie emulator jedynego słusznego systemu dla biednych ludzi takich jak ja. Androida znaczy. 

Do tej pory używałem standardowego narzędzia dostarczanego z Android Studio. Zauważyłem jednak jego "mulastość" oraz problemy z zawieszaniem się na moim Kubuntu. Siłą rzeczy co jakiś czas musiałem go restartować. Dziwnie też działała rotacja ekranu.

## Genymotion
Przeglądając dokumentację React Native zwróciłem uwagę, że polecanym emulatorem nie jest ten, którego używam, a całkowicie osobny produkt o nazwie [Genymotion](https://www.genymotion.com/fun-zone/). Kliknąłem linka, przeczytałem co oferuje, zainstalowałem. W przeciwieństwie do innych alternatywnych emulatorów, Genymotion jest dedykowany deweloperom i __działa na Windows, Mac OS oraz Linux__.

### Virtual Box, k**wa!
Nie ruszysz, jeśli nie masz go zainstalowanego. Niby nic specjalnego na deweloperskiej maszynie, ale ja, po przesiadce z Vagrant na Docker, byłem przekonany, że się Virtual Boxa definitywnie pozbyłem. Ot, sarkastyczny żart Pani Naiwności.

Koniec końców emulator zaprezenotwał mi się w swojej pełnej krasie:

![Native Report w emulatorze Genymotion](/images/genymotion-screen-nr-1.jpg)


## Tylko dla niekomercyjnych projetów
Emulator ten można uzywać bezpłatnie jedynie na własny użytek, a za komercyjne użycie trzeba zapłacić. Na dzień dzisiejszy (maj 2017) jest to 99 euro za rok, więc trzeba samego siebie zapytać, czy jego wydajność oraz dodatkowe funkcjonalności zawarte w płatnej wersji mają dla nas aż takie znaczenie.

## Co polubiłem w Genymotion?
* __Nie zawiesza się__ 1111111,
* Bardzo dobrze działa obsługa kamery,
* Łatwa konfiguracja emulacji konkretnego modelu telefonu. A modeli mamy do wyboru ponad 40,
* Symulowanie niskiego zużycia baterii,
* Symulacja GPS dzięki czemu możemy testować aplikacje wykorzystujące geolokalizację.

## Co mnie nastawia sceptycznie?
* Koszt komercyjnej licencji w wysokości 99 Euro / rok,
* Zrzuty ekranu dostępne tylko w komercyjnej wersji,
* Wymaga zainstalowanego Virtual Box.

## Werdykt
Pierwsze wrażenie bardzo pozytywne, ciekaw jestem jak będzie mi się dalej pracowało z Genymotion. Może zauroczy mnie do tego stopnia, że przejdę na Pro?    
Na pewno zanotuję na tym blogu, jeśli odkryję coś istotnego w pracy z tym emulatorem.