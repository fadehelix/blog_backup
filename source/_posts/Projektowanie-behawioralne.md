title: Projektowanie behawioralne
author: Adam Dziendziel
tags:
  - BDD
  - DSP2017
  - Cucumber
  - Gherkin
  - Agile
categories:
  - Tech
date: 2017-03-14 13:55:00
---
![](/images/02-specification-by-example-coffee.jpg)

Przyznam szczerze, że nie mam jeszcze ścisłego planu na rozwój [Native Report](https://github.com/fadehelix/nativereport).
Wiem w jakiej technologii chcę ją wykonać  i wiem co docelowo chcę aby umożliwiała użytkownikowi, natomiast nad detalami funkcjonalnymi zastanawiać się będę w trakcie rozwoju projektu. Czyli wg Dave'a Snowdena projekt jest [złożony](https://www.mindtools.com/pages/article/cynefin-framework.htm). 
![](/images/02-cynefin-model.jpg)

Tak na marginesie polecam każdemu zapoznać się z frameworkiem Cynefin, bo pozwala świadomie dobrać metodologię i narzędzia do projektu i, na przykład, uniknąć wdrażania scruma tam, gdzie lepiej sprawdzi się nawet ten ponury... w a t e r f a l l. Tfu, wypowiedziałem to słowo! 
_Dzwonek, kurtyna opadła szarpanym ruchem, autor wziął chwilę przerwy na płukanie jamy ustnej._



Lista funckjonalności
---------------
_Kurtyna się podniosła, autor jeszcze od czasu do czasu mlaska z niesmakiem._

Jeśli nie mam planu od A do Z, to mogę pokusic się tutaj o zaczerpnięcie z rozwiązań, uwaga, modne słowo, "edżajlowych". Z racji tego, że pracuję sam i projekt jest mały, to konfigurowanie scruma (który przez wiele osób jest zamiennie stosowany z terminem "agile") uważam za nadmiarowe. Pokazuję tutaj środkowy palec nawet powabnej i uwodzicielskiej idei sprintów (nie ma tutaj osobnego stackholdera),  natomiast chętnie użyję [historyjek użytkownika](http://www.agilemodeling.com/artifacts/userStory.htm).
Powinienem jeszcze nieśmiale dodać, że kanbana też nie chcę mi się utrzymywać.
Serio? To jakim cudem historyjki użytkownika mają wciąż sens?

Czy słyszeliście o [Behavior Driven Development](https://www.agilealliance.org/glossary/bdd/)? No więc jest taki gość, Gojko Adzic, który lubi na to używać określenia "Specification by example". Napisał nawet [książkę o takim tytule](https://gojko.net/books/specification-by-example/). Lubię ją, bo teorii w sumie niewiele, sporo obrazków i dużo praktycznych przykładów z różnych projektów i firm.
Mi ta książka dała lepsze zrozumienie sensu BDD, ponieważ autor koncentruje się na projektowaniu apikacji a nie narzędziach.
Wcześniej BDD to były dla mnie takie frameworki jak Cucumber i Behat służące do testów funkcjonalnych. Ba, uczestniczyłem pewnego razu w projekcie, gdzie "ogórkowe" scenariusze oprócz klikania po aplikacji za pomocą Webdrivera sprawdzały jeszcze głęboko zaszytą logikę aplikacji, taką jak np. stany bazy danych. 

Problem w tym, że testy behawioralne na tak niskim poziomie stają się bardzo drogie i skomplikowane w utrzymaniu i często ich sens jest kwestionowany, bo przecież są testy jednostkowe i testerzy manualni w Indiach.

_Rozbłyskują reflektory, na scenie pojawia się wreszcie główny bohater_

Adzic w swojej książce użył terminu "Living documentation" jako sposobu na postrzeganie scenariuszy, które de facto stają się  historyjkami uzytkownika (user stories).
Chodzi o to, że zamiast skupiać się na detalach takich jak np. konkretne pola w formularzu, czy rodzaju przycisku, koncentrujemy się na celu biznesowym. Dla użytkownika (lub właściciela strony, zależy od użytego kontekstu) ważne jest, że może zarejestrować się na stronie poprzez formularz, natomiast pola w nim są już mniej istotne.


Do definiowania "ficzerów" (tak,tak to się nazywa w Cucumber) służy "[BusinessReadableDSL](https://martinfowler.com/bliki/BusinessReadableDSL.html)" zwany [gherkin](https://github.com/cucumber/cucumber/wiki/Gherkin).
Oto przykład:

```gherkin
Scenario: Get list of projects
    Given I am on the welcome screen
    When I login
    Then I see the list of available projects
```
Mamy tutaj trzy słowa kluczowe: 
- __Given__: definiuje stan początkowy
- __When__: opisuje warunek jaki musi spełnić "aktor"
- __Then__: Cel biznesowy. Powinien to zawsze być stan aplikacji, a nie czynność.

Dlaczego to jest dobry przykład specyfikacji?
- Koncentruje się na celu użytkownika: wyswietlenie listy dostepnych projektów,
- Nie zawiera detali takich jak np. pola formularza logowania: dzięki temu testowanie jest tańsze, bo nie wchodząc w szczegóły łatwiej jest aktualizować skrypty testujące,
- Jest niezależna od innych,
- Jest krótka, a więc konkretna i czytelna,
- Można ją zamplementować przed developmentem, bo nie musimy znać szczegółowej struktury html testowanej aplikacji.


Jeszcze raz powtórzę: __moim zamiarem jest utworzenie łatwej do utrzymania, aktualnej i zorzumiałej dla nietechnicznej osoby dokumentacji funckjonalnej projektu__, a nie tworzenie precyzyjnych scenariuszy testowych.
W przyszłości jeszcze na pewno wrócę do pisania "ficzerów" w kontekście testów funckjonalnych.

Aby nasza dokumentajcja w postaci ficzerów była dostępna dla każdego zainteresowanego można użyć takieo narzędzia jak [Relish](https://www.relishapp.com/). Dzięki temu z poziomu przeglądarki internetowej możemy sobie wygodnie przeglądać i czytać naszą _lajving dokumentejszyn_.

To tyle nudnego teoretycznego wstępu. W następnym poście przedstawię konfigurację Cucumber + Calabash i pokażę jak "ożywić" nasze ficzery.

_Kurtyna opadła, zabrzmiał dzwonek_

__Słowo od suflera__  
Pisząc tego posta zacząłem się zastanawiać jaka jest poprawna forma zapisu: _behavior_ czy _behaviour_? Okazuje się, że obie, z tym że ta wersja bez “u”, czyli _behavior_ jest to słowo z amerykańskiego angielskiego. W reszcie anglojęzycznych krajów piszemy _behaviour_. Ja wolę tą pierwszą odmianę, bo jest prostsza w zapisie i wymowie. W końcu Amerykanie to pragmatyczny naród.



__Linkografia__  
[Świetna prezentacja o BDD i Cucumber](https://www.youtube.com/watch?v=fzKEfqenbhk)  
[Relish - Repozytorium “ficzerów”](https://www.relishapp.com/)  
["Specification by Example" by Gojko Adzic](https://gojko.net/books/specification-by-example/)   
[Krótkie wprowadzenie do Cynefin](https://www.youtube.com/watch?v=N7oz366X0-8)