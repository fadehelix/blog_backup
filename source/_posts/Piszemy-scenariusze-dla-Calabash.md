title: Pierwszy scenariusz z wykorzystaniem Calabash
author: Adam Dziendziel
tags:
  - Cucumber
  - DSP2017
  - Calabash
  - Gherkin
categories:
  - Tech
date: 2017-04-16 13:54:00
---
![]](/images/piszemy-scenariusze-banner.jpg)

Dzisiaj przyszedł czas na zdefiniowanie pierwszej funckjonalności aplikacji.

### Organizacja ficzerów
Jakiś czas zastanawiałem się nad “szczegółowością” scenariuszy, bo z jednej strony natura testera kieruje mnie w stronę precyzyjnie zdefiniowanych kroków (ang. steps), a jednocześnie potrzeba posiadania specyfikacji koncentrującej się na celach biznesowych składnia mnie do maksymalnego ukrycia detali.

Oczywiście jednym z rozwiązań jest podział na katalogi i dlatego tworzę folder _features/specification_ dla "Living documentation".

Drugim rozwiązaniem są [tagi](https://github.com/cucumber/cucumber/wiki/Tags), które same w sobie na nic nie wpływają (nie ma predefiniowanych akcji dla konkretnych tagów), ale można samemu napisać ich obsługę. Dodatkowo, uruchamiając testy można polecić, aby zostały wywołane tylko ficzery (oraz scenariusze) oznaczone podanym tagiem, np.   
```
$ calabash-android run app/build/outputs/apk/app-debug.apk -t @specification -t @jobs
```


Podwójny parametr _-t_ odpowiada operacji logicznej _AND_.


### Predefiniowane stepy
Tworząc specyfikację można użyć gotowych definicji czynności i asercji:
https://github.com/calabash/calabash-android/blob/master/ruby-gem/lib/calabash-android/canned_steps.md

Zajduja się tutaj: ~/.rvm/gems/ruby-2.3.3/gems/calabash-android-0.9.0/lib/calabash-android/steps

Są one przede wszystkim świetnym źródłem inspiracji, szczególnie dla kogoś nie znającego Ruby. Tak, mówię o sobie ;) 

### Specyfikacja
Ok, czas na odpalenie edytora i napisania wreszcie trochę (pseudo) kodu.
Najpierw tworzę katalog features/specification aby oddzielić ogólną [“żywą” dokumentację](https://www.relishapp.com/relish/relish/docs/living-documentation) od bardziej technicznych testów funkcjonalnych.   
Następnie definiuję ficzer wyświetlający listę zleceń: [job_list.feature](https://github.com/fadehelix/NativeReport/blob/master/android/features/specification/job_list.feature)
```Gherkin
@specification @jobs
Feature: Job list
  I order to organize my work today
  As a user
  I want to see all jobs assigned to me

  Scenario: Show all jobs
    Given I am on job list
    Then I see all jobs assigned to me

  Scenario: Show only today’s jobs
    Given I am on job list
    When I use "today" jobs filter
    Then I see all jobs assigned to me today

  Scenario: Show finished jobs
    Given I am on job list
    When I use "finished" jobs filter
    Then I see all jobs finished by me
```
Mała dygresja: definiowanie takich scenariuszy pozwala nam skupić się na małych fragmentach aplikacji, które dostarczają konkretną wartość użytkownikowi (a tym samym klientowi).   
Dzięki temu rozmowa w zespole jest bardziej precyzyjna i możemy przewidzieć więcej potencjalnych problemów lub ścieżek rozwoju.

A teraz czas na wytłumaczenie co ja tu właściwie naklepałem.   
Pierwsza linijka to [tagi](https://github.com/cucumber/cucumber/wiki/Tags) dotyczące ficzera. Pozwalają nam one lepiej zorganizować ficzery niezależnie od struktury katalogów (sam nie jestem pewien, czy dobrym pomysłem jest tag “specification” skoro używam dla dokumentacji osobnego katalogu).   
Główna zaleta tagów jest taka, że możemy sobie wybierać grupy ficzerów, które chcemy (lub nie) uruchamiać w Calabash.   

Sekcja zaczynająca się od słowa kluczowego __Feature__ opisuje funckjonalność. Mamy tutaj pełną dowolność w opisie, ale dobrym zwyczajem jest stosować konwencję historyjki użytkownika, która tłumaczy kontekst biznesowy i określa "narratora" historyjki.

Następnie mamy konkretne __scenariusze__, które modyfikują nam wejściowe założenia i efekt. W powyższym przykładzie jest to użycie filtru, który ma wyświetlić tylko konkretne zlecenia.


### Piszemy własne stepy
Calabash dostarcza nam zestaw predefiniowanych stepów, które są świetne jeśli chcemy pisać scenariusze testowe zrozumiałe dla zespołu deweloperskiego, ponieważ bardzo precyzyjnie opisują każdą czynność wykonywaną na aplikacji:   
```
I press the menu key
I swipe right
I see "przykładowy tekst"
```

Natomiast, jeśli chcemy napisać specyfikację funkcjonalną, warto zdefiniować własne, bardziej ogólne ale specyficzne dla aplikacji, stepy podpierając się implementacją "gotowców". Na przykład chcę mieć 
```gherkin 
Given I am on job list
```
Najprostsza implementacja w pliku _calabash_steps.rb_ może wyglądać tak:
```ruby
Then /^I am on job list$/ do
  pending
end
```
Ta implementacja robi... nic. A to dlatego, że w tej iteracji nie mam jeszcze stworzonej funkcjonalności (Lista zleceń) więc nie mam jak zweryfikować, czy powyższa asercja w ogóle zadziała. Słowem, jestem zwolennikiem równoległego  implementowania scenariuszy testowych oraz testowanej funkcojalności w aplikacji.

Aby wyraźnie taki stan rzeczy zaznaczyć w dokumentacji możemy, przy ficzerze, lub konkretnym scenariuszu, użyć tagu _@wip_ oznaczającego "work in progress", albo innego _@todo_. 

### Relish jako przeglądarka dokumentacji

[Relish](https://relishapp.com) jest tym, co czyni nasze scenariusze tzw. "[Living documentation](/Projektowanie-behawiralne)" ponieważ pozwala je przeglądać każdemu w przeglądarce internetowej.  
Ważne, aby sobie uświadomić iż jest to narzędzie dla osób nietechnicznych - nie mamy tutaj informacji o stanie testów, a jedynie możemy czytać scenariusze, które w wygodny sposób można wyszukiwać.   
Przed następnymi krokami musimy tam założyć konto, które dla projektów publicznych jest darmowe.

__Instalacja__   
Przede wszytkim instaluję gema relish: `$ gem install relish`   
W katalogu _NativeReport/android_ dodajemy projekt: `$ relish projects:add uzytkownik/native-report`

__Publikacja__   
W celu uploadu naszych ficzerów na relish wykonujemy: `$ relish push uzytkownik/native-report`

Zobacz jak wygląda mój [ficzer opisujący listę zleceń](https://relishapp.com/fadehelix/native-report/docs/specification/job-list)

Mogę oczywiście polepszyć "user experience" dokumentacji poprzez stworzenie [dodatkowego opisu](https://relishapp.com/relish/relish/docs/client-gem/markdown-files) oraz [dostosowanie nazw plików i katalogów widzianych w relish](https://relishapp.com/relish/relish/docs/client-gem/nav-file). Narazie wystarczy mi najprostsza forma.

Co jeszcze uważam za ogromy plus tego rozwiązania to możliwość wydrukowania dokumentacji. Mi osobiście dobrze się to czyta w .pdf.

### Hasztag empatia
Na koniec mała dygresja.  
Mój pierwszy kontakt z Cucumber nastąpił w projekcie, gdzie definiowaliśmy scenariusze pisząc je w trzeciej osobie, np. `He clicks the "submit" button`, w końcu pisaliśmy o uzytkowniku.   
Później jednak, aby uprościć sobie pracę, zacząłem używać DSL [Capybara](https://github.com/teamcapybara/capybara) i tam są definicje w pierwszej osobie. W Calabash mamy podobnie. Najpierw pomyślałem, że to po prostu wygodniej z punktu widzenia gramatyki (wiecie, odpadają wszystkie te "s" doklejane do czasowników w trzeciej osobie liczby pojedynczej), a dopiero później dotarło do mnie, że taka forma daje nam coś więcej.    
Pisząc "I wanto to do sth", "I see sth" automatycznie wchodzimy w skórę użytkownika, przez co łatwiej nam wyobrazić sobie czy np. to, co projektujemy w ogóle ma sens. Stajemy się bardziej odpowiedzialni i zaangażowani. Łatwiej nam też końcowego użytkownika zrozumieć i nie traktować go jak wroga/szkodnika/idiotę/wstaw swoje ulubione pejoratywne określenie.


### Ciekawostki
__Języki__   
Komenda `$ cucumber i18n pl` Wyświetla wszystkie słowa kluczowe w danym języku (w tym przypadku po polsku). Przydatne jeśli pracujemy dla (polskiego) klienta, lub piszemy artykuł o Cucumber ;)

__RubyMine by pisało się lepiej__   
Fajnie by było w specyfikacji móc klikać w stepa aby przejść do jego definicji. Mocno to upraszcza analizę oraz pisanie własnych implementacji. To jest Cucumber, a więc Ruby.   
Moimi głównymi narzędziami pracy są Vim i Phpstorm, ale zdarza mi się użyć Visual Studio Code lub Atoma (do frontendowych spraw nadają się świetnie a są open source). Niestety nie zauważyłem, aby któreś z tych środowisk wspierało Ruby więcej, niż kolorując składnię.   
No więc... instaluję triala [RubyMine](https://www.jetbrains.com/ruby), tworzę w nim projekt w katalogu _./features_  i zabieram się do pisania scenariuszy.
Najpierw piszemy stepa, który zostanie podświetlony na żółto, bo edytor nie może znaleźć implementacji. Nie może bo jej niema, logiczne, więc gdy kursor znajduje się na podświetlonym, naciskamy `alt+enter` i tworzymy definicje wybierając plik _calabash__steps.rb_. 

__Page Object Pattern__   
Eleganckim i elastycznym sposobem rozwijania architektury testów funkcjonalnych/integracyjnych jest napisanie sobie DSL w oparciu o [model Page-Object](https://rubygemtsl.com/2014/01/06/designing-maintainable-calabash-tests-using-screen-objects-2/).    
W Calabash mamy ekrany (_ang. screen_), które możemy sobie zmapować do klasy i trzymać w niej właściwości (pola, przyciski itp), oraz metody (akcje). Pozwala to przede wszystkim na zwiększenie czytelności kodu testów i silną redukcję bałaganu jaki zawsze pojawia się wraz z dopisywaniem kolejnych funkcjonalności.      
Do tematu powrócę w przyszłości w któreś z kolejnych iteracji rozwoju aplikacji.

### Linki: 
[Mind Mapa ficzerów w projekcie](https://bubbl.us/Mzk3NTA3OS83ODU4ODgxLzZjNWEyYTY4YjEwODc4MTEzYjNlNWI5YzUxOWZhYmQz-X?s=7858881)   
[Dokumentacja Cucumber](https://github.com/cucumber/cucumber/wiki/A-Table-Of-Content)   
[Tagi w Cucumber](https://github.com/cucumber/cucumber/wiki/Tags)   
[Screen Object Pattern](https://github.com/calabash/x-platform-example)