title: Myślenie analityczne a kreatywne
author: Adam Dziendziel
tags:
  - DSP2017
  - IT
categories:
  - Ludzie
date: 2017-05-23 22:59:00
---
![Zdjęcie pobrane z pexels.com](/images/analityka-kreatywnosc-intro.jpeg)
Dzisiaj krótki tekst o tym jak __nie być__ efektywnym programistą. Jest to taka nieśmiała i trochę chaotyczna próba zrozumienia problemów jakie miałem [implementując nawigację](/React-Native-Nawigacja/) w aplikacji [Native Report](https://github.com/fadehelix/native-report). Jest to chyba także podsumowanie wywalenia się mojej "kariery" developera o ścianę. Taką z bardzo solidnych cegieł, nie tych pustaków z trocin co to je teraz robio Kazki budownictwa. 


## Ja mam mózg, Ty masz mózg, wszyscy mają mózg!
Dla niektórych to może być szok, ale to naukowo dowiedziona prawda. Każdy posiada swój własny, prawdziwy mózg.    
To, co mnie osobiście zainteresowało w tym temacie, to fakt, że mamy dwie półkule, z których, generalizując, lewa odpowiada za myślenie analityczne, a  prawa za kreatywne. No i teraz wchodzi do gry kwestia tego, która półkula dominuje u danej osoby.

![](/images/kreatywnosc-analitycznosc-mozg.png)

Gdyby porównanie z powyższej grafiki odnieść do zawodowej rzeczywistości w IT, to tak naprawdę mało jest miejsca dla osób z domunijącą prawą półkulą. No bo tak:
* programista - podstawa to myślenie analityczne. Wyczucie czasu jest bardzo ważne przy estymacji zadań i ich skutecznej realizacji. I jeszcze z doświadczenia wiem, że religijność też jest na plus, bo każde wsparcie przydaje się podczas robionego na siłę piątkowego deploya na produkcji. Jednocześnie dobry programista musi twardo stać na ziemi i dociekać wszelkich potencjalnych słabych punktów w projekcie.
* menedżer projektu musi z kolei umieć planować, być zorganizowany, musi bardzo precyzyjnie przestawiać swoją wizję. Nie ma tu miejsca na metafory. No i musi umieć liczyć czas i budżet.
* designer to być może niespodzianka, ale serio, dobry projektant stron i aplikacji internetowych to jest bardziej dobry rzemieślnik podejmujący racjonalne decyzje i umiejący je wytłumaczyć reszczcie zespołu plus klientowi, niż kierujący się swoją własną nieprzetłumaczalną wizją artysta. Ci bardziej kreatywni świetnie za to sprawdzają się choćby w branży game devu.

No i podstawa w zespołach IT, czyli precyzyjna, racjonalna komunikacja, oraz umiejętność pracy pod ciągłą presją czasu.

Koniec tego przydługiego wstępu, zapraszam do głównej części programu.

## Nauka nowej technologii
Jeśli uczyniłeś mi ten honor i przejrzałeś zawartość niniejszego bloga, to być może zauważyłeś, że dopiero [uczę się React oraz React Native](/rzybijam-piatke-z-React-Native/). Uczę się praktycznie od podstaw, wliczając w to naukę od nowa javascript, że o ES6 nie wspomnę.
No bo umówmy się, jQuery którego wymagał ode mnie przez parę lat Drupal to tyle ma wspólnego z kodowaniem w JS, co Internet Explorer z przeglądarką internetową.

Specyficzny dla React jest fakt, iż jest to cały ekosystem bardzo dynamicznie ewoluujący. Nie ma tu miejsca dla kreacjonistów, którzy wyznają stworzenie przez jednego Ojca jak to ma miejsce np. w pehapowym frameworku Laravel.   
Co prawda za React stoi Facebook ale to też jest zespół developerów, którzy muszą negocjować choćby tylko ze sobą.

No więc wszystko się zmienia i to bardzo szybko. Zmienia się sama biblioteka, zmieniają się i powstają nowe narzędzia. Przy takiej dynamice, że tutoriale sprzed roku są "deprecated" nasze wybory to bardziej kwestia intuicji, niż chłodna kalkulacja. Moja prawa półkula mózgu lubi to.



## Cierpliwość
Bezpośrednim powodem napisania tego posta jest moja przygoda z biblioteką [react-navigation](https://reactnavigation.org/) i implementacja nawigacji pomiędzy listą zleceń, a szczególami wybranej pozycji. Lista ma jeszcze zakładkową (_ang. tabs_) "subnawigację" służącą do filtowania zleceń.

Na ten moment wygląda to tak:
![NativeReport w emulatorze](/images/analityka-kreatywnosc-screen-1.png)

O ile wybór tej biblioteki był trafny, to [wpakowanie się w przygodę z Redux](/React-Native-i-Redux) był... mocno optymistyczny. A na pewno nierozsądny i nieuzasadniony. Po paru godzinach nierównej walki z zagnieżdżonymi Navigatorami i próbą zorientowania się w powodach błędów, którymi aplikacja sypała, zrobiłem to, co typowy programista zrobiłby od  razu: __systematycznie przeanalizowałem dokumentację i przykłady implementacji react-navigation__. Dzięki temu dowiedziałem się, że _navigator_ bardzo dobrze zarządza swoim stanem i operowanie na nim jest łatwiejsze, niż zewnętrznym magazynem stanów.

Słowem, zamiast bezrefleksyjnego [nalotu dywanowego](https://pl.wikipedia.org/wiki/Nalot_dywanowy) (nauki dywanowej?) polegającego w tym przypadku na znalezieniu jak najszybciej jak największej ilości rozwiązań i wybraniu czegoś, co mi pasuje, powinienem przeczytać dokumentację jednego rozwiązania od początku do końca. Nie zakładając, nie przewidując, po prostu analizując co ta konkretna biblioteka faktycznie dostarcza i czego jej brakuje. 

Analityk 1 : Kreatywny 0


## Minimalizm
Dodanie każdej nowej biblioteki do projektu, zwiększa dług technologiczny. Inaczej to się rozpatruje, gdy znamy tą bibliotekę, a inaczej, gdy używamy jej pierwszy raz. W pierwszym przypadku możemy sobie ryzyko oszacować, w drugim lecim yolo i lepiej w tej sytuacji mieć wyrozumiałego product ownera / klienta / szefa.

Skoro wiem jak powinienem podchodzić do nowego tematu i nawet tą wiedzę potrafię stosować, to dlaczego wciąż powtarzam ten błąd i na wejściu próbuję chwycić kilka srok za jeden ogon?   
Bo prawdopodobnie mój wewnętrzny motorniczy tramwaju zwanego Adaś nie postrzega tego jako błąd. Nie w sensie ścisłym.   
Za każdym razem jestem święcie przekonany, że przeskakując na inne rozwiązanie zyskam czas. Za każdym razem święcie wierzę, że wystarczy przysłowiowy `$ npm i redux --save` i mój problem zniknie.     
Moja lewa półkula w tym momencie trzeszczy i iskrzy świadoma tego, co takie podejście powodowało w przeszłości, ale liczy się adrenalina, kopa daje eksploracja nieznanych obszarów. Liczy się to, że mały Adaś dostał nowe klocki do kolekcji i będzie mógł z nich tworzyć jeszcze większe budowle.     

A na końcu przychodzi ktoś dorosły z kwaśną miną, źrenicami jak pięć złotych i wkładając potężny wysiłek w opanowanie swoich nerwów, mówi: masz natychmiast posprzątać ten bałagan! I co zrobiłeś z moim portfelem!?.


## Offline mode
{% instagram BURIXj0jGWz %}

Przekonałem się, że jednym z niewielu skutecznych sposobów na polepszenie mojej koncentracji jest wyłączenie internetu. Jestem tak stary, że pamiętam jeszcze czasy, gdy internet miało tylko paru znajomych, więc szło się do kafejek internetowych albo wykorzystywało do maksimum lekcje informatyki w technikum.

Sposób działania mam taki, że zapisuję sobie potrzebne strony (dokumentację) w [Pocket](https://getpocket.com), lub [Instapaper](https://www.instapaper.com/) (pozwala "zakreślać" tekst) dzięki czemu mam je dostępne na telefonie. Oczywiście telefon też mam offline. Można też zapisać stronę jako pdf i czytać na laptopie, ale jeśli nie ma dużo kodu, to na telefonie dobrze mi się czyta.

Idę sobie z telefonem i laptopem w jakieś ustronne miejsce i koncentruję się tylko na zrozumieniu wybranej (jednej!) biblioteki. No i muszę bardziej używać analitycznego myślenia, bo Stack Overflow został za firewallem.


## Sens
Dlaczego w ogóle napisałem tyle o mózgu, o tym jak to ja bardzo się nienadaję do tej roboty, chociaż dalej ją robię, więc czemu w takim razie jęczę zamiast coś w swoim życiu zmienić porzucić strefę komfortu zacząć ścigać swoje marzenia? Uff.

Bo bardzo tą branżę lubię. Uwielbiam jej dynamikę, zmienność, interdyscyplinarność, fakt, że każdy projekt  jest inny i można się nauczyć czegoś nowego zarówno w obszarze technologii jak i biznesu. Uwielbiam poznawać ludzi, którzy często z wykształcenia są zupełnie kimś innym, niż informatyk i wnoszą inny punkt  widzenia oraz inne doświadczenia do projektów. Uwielbiam to, że siedząc sobie w moim ukochanym Bielsku mogę jednocześnie pracować z ludźmi z całego świata.

Tak naprawdę najtrudniejsze jest, aby znaleźć sobie na tym pokładzie miejsce, które pozwoli mi mieć poczucie przynoszenia korzyści reszcie zespołu i klientowi.

Być jak Pan Nutt w "Niewidocznych Akademikach" Pratchetta.