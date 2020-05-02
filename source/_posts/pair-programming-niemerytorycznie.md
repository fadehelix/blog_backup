title: Niemerytorycznie o pair programming
author: Adam Dziendziel
tags:
  - Agile
  - DSP2017
  - XP
categories:
  - Ludzie
date: 2017-05-15 06:53:00
---
![Źródło pexels.com](/images/pair-programming-intro.jpg)

Recz działa się pewnego listopadowego popołudnia we Wrocławiu. Nienawidzę listopada z uwagi na jego szarość, zimno i widmo nadciągającej zimy. Zima w mieście, nawet tak pełnym dobrej energii i uroku, jak Wrocław, jest strasznie depresyjna.    
Nie wiem jak Ty, drogi czytelniku, ja o tej porze roku mam jedno marzenie: zostać Panem Jeżem Który Ma Wyjebane. Marzę sobie, że mam na całym ciele kolce które trzymają inne mroczne stwory na dystans, że znajduję sobie stertę pachnących kolorowych liści i zakopuję się w nich zapominając o świecie aż do wiosny.   
O, właśnie tak jak ten tutaj:

![Jeż z Ośrodka Rehabilitacji Jeży "Jerzy dla Jeży" w Kłodzku](/images/pan-jez-a.jpg)

No więc właśnie w takich okolicznościach rozgrywa się dzisiejsza opowieść. Ona wydarzyła się naprawdę. Ta opowieść. Kiedyś. 
Skoro miejsce i czas akcji są Ci już znane czas na przedstawienie głównych bohaterów. To jest w ogóle dość zabawne, bo drugoplanowi bohaterowie są tak naprawdę tutaj ważniejsi, niż główni, no ale to kobiety, więc nie mogą być ważniejsze od nas, mężczyzn. Wiesz jak jest -  Korwinistyka i te sprawy. Zazwyczaj bardzo trudne,a  często trochę wstydliwe. Te sprawy. 

To może ja zacznę od głównych bohaterów, tych, którzy są tutaj tak naprawdę mniej  ważni niż drugoplanowi. 


## Było nas dwóch, w każdym z nas inna krew

Poznaj... mnie! No elo.  Tutaj występuję w roli tego, inżyniera testów automatycznych slesz testera manualnego.   
Poznaj Stefana (alias dla postaci autentycznej). Programista z długoletnim doświadczeniem, prawdziwy inżynier oprogramowania wciąż potrafiący się pasjonować swoją pracą.

Pracowaliśmy w tym samym projekcie, wśród zgrai turbo mózgów, gości, którym ja się wstydziłem buty czyścić. Przynajmniej jeśli chodzi o apsekty techniczne, bo z [tymi miękkimi](https://en.wikipedia.org/wiki/Soft_skills) było miękko. No ale w sumie po co gadać, skoro tu się robi. To wciąż jest problem w wielu zespołach, a im wyższy jest poziom techniczny, tym bardziej umiejętności nietechniczne są deprecjonowane. 

No więc byłem sobie ja i Stefan. Stefan i ja. My dwaj.   
A dlaczego akurat on, a nie ktoś inny z zespołu?   
Ponieważ... siedzieliśmy biurko w biurko w taki sposób, że widzieliśmy swoje monitory. My musieliśmy ze sobą dobrze żyć, albo skończyłoby się to katastrofą dla któregoś z nas.   
No dobrze, to był czerstwy żart.    
Bo Stefana wyróżniała jedna cecha: chciał i lubił pomagać innym, nawet jeśli czasem odbywało się to kosztem jego wydajności w projekcie.   
Ja też lubię pomagać innym, wspierać ich w rozwoju, więc relację zawodową mogliśmy zbudować na jakieś konkretnej wartości,  która była istotna dla nas obu.   
Różniła nas mentalność. On introwertyk, a ja jednak dość mocno się uzewnętrzniam.   
No więc byłem sobie ja i Stefan. Stefan i ja. My dwaj.

Pamiętam, że było już ciemno, gdy zostaliśmy sami w biurze. Marmurowe twarze spoglądały na nas szyderczo ze swoich miejsc na wysokich kolumnach (bo musisz wiedzieć, że to było biuro w pięknej zabytkowej kamienicy a to konkretne pomieszczenie było ongiś salą balową. Taką, gdzie ludzie tańczyli i pili, a muzyka napędzała ich swawole ).  

No więc siedzieliśmy sami w pustej sali balowej.    
Spojrzeliśmy na siebie. On kończył swojego taska. Ja klnąłem, że znów testy bez wyraźniego powodu się wywalają. On zaproponował, że mi pomoże. Ja klnąłem dalej. On skończył swojego taska i spojrzał na mój monitor. Ja oddałem mu swoją klawiaturę ostatnim ruchem myszki włączając youtube.  

I tutaj krótka merytoryczna dygresja, dla tych którzy nie do końca rozumieją kontekst i mogą sobie coś niewłaściwego pomyśleć o nas.

## Pair programming
Tak, ja wiem, że ta metodyka ma polskie tłumaczenie i masz całkowitą rację marszcząc czoło i plując na swój monitor, ale oryginał brzmi lepiej, niż "programowanie w parze". Szczególnie, że to dwóch facetów programowało w parze ze sobą.   
 I każdy z nich mial swoją, chowaną w kuchni, dziewczynę. I co ta niewiasta by potem miała powiedzieć słysząc, że jej wybranek ODBYWAŁ SESJĘ programowania W PARZE ? No ja jej współczuję. Lepiej się zawczasu rozejrzeć za wygodną kanapą.   
A  po angielsku brzmi to mniej dosłownie i jakoś tak... bezpieczniej? Z tego, co mówił Krul to kobiety nie powinny znać języków obcych.

Ej, mordo, ale miało być merytorycznie!    
Taaaaa, poczekaj chwilę, odetchnij głębiej i pozwól mi wziąć łyk kawy.

[Pair programming](https://www.agilealliance.org/glossary/pairing/) to metodyka polegająca na tym, że dwóch programistów siada przy jednym komputerze i na zmianę "prowadzą" i "pilotują". Coś jak w samochodzie raidowym, ale tutaj metafora nie jest ścisła, bo obaj w równym stopniu są pilotami. Ale tylko jeden w danym momencie kontroluje klawiaturę.

Fantastycznie to jest pokazane przez jednego z moich ulubionych "jutuberów" @mpj a.k.a [funfunfunction](https://www.youtube.com/channel/UCO1cgjhGzsSYb1rsB4bFe4Q)   
{% youtube zFO1cRr5-qY %}

Pracując w parze (tak, wiem, wiem co napisałem chwilę wcześniej, ale Pani z Polskiego mówiła, że nie można powtarzać wyrazów, bo dostaniesz minusika) pracujemy wolniej, niż w pojedynkę, ale:

__.uczymy się dużo od siebie__ - poziom całego zespołu idzie w górę , 

__.rozmawiamy na głos o problemie__ który rozwiązujemy, co pozwala nam spojrzeć na niego z szerszej prespektywy,

__.zmiejszamy czas potrzebny na review omawianego kodu.__ Robicie [code review](https://nafrontendzie.pl/dlaczego-warto-praktykowac-code-review/), prawda? PRAWDA !?

__.zniwelowanie ryzyka związanego z posiadaniem tzw. "rambo dewelopera"__ znanego też jako ["rock star developer"](http://www.henryalgus.com/managing-rock-star-developers/), czyli sytuacji w której tylko jedna osoba ma ogromną wiedzę o projekcie przez co jest ona niezbędna, a gdy jej zabraknie to pojawiają się ogromne problemy nawet z prostymi zadaniami. No i projekt jest zależny od humorów tej osoby.

__.można się lepiej poznać.__ I nie chodzi mi tutaj nawet o oczywiste względy osobiste, ale lepiej możemy zrozumieć, czy zaobserwować sposób myślenia drugiej osoby. Może się nagle okazać, że ktoś o mniejszych umiejętnościach świetnie umie rozwiązywać problemy, ale znajdywać kreatywne rozwiązania.

__.ćwiczenie skutecznej komunikacji__ i wyrażania swoich myśli u introwertycznych z natury programistów. Bezcenne.

## Sesja wakawaka
Czyli postanowiliśmy po prostu rozwiązać problemy w testach poprzez wspólną pracę. Tylko skąd ten youtube się tam wziął? I gdzie ci drugopanowi bohaterowie? To chyba nie te twarze śmiejące się z kolumn?

Zanim przejdę do rzeczy, pragnę wyraźnie zaznaczyć jedno: ja zazwyczaj słucham ciekawszej muzyki, w stylu jazz, trochę klasycznej, czasem się jakiś dobry rap trafi. Stefan też raczej gustuje w muzyce pobudzającej mózg i wyobraźnię.   
Jednak tym razem postanowiłem pójść po totalnej bandzie i tak oto na scenę wkraczają drugoplanowe bohaterki tej historii:

__Shakira__   
{% youtube pRpeEdMmmQ0 %}

oraz 

 __Ellie Goulding__   
 {% youtube CGyEd0aKWZE %}
 
 Idea od początku była taka, żeby puścić __na głośnikach__ coś głupiego, coś co poleci sobie w tle, da nam prostej energii. Coś jak z lizaniem kostek cukru - niby niezdrowe i trzeba myć potem zęby, ale ile daje naturalnej przyjemności!   
 Zamiast próbować zdominować się nawzajem swoimi gustami muzycznymi zaczęliśmy prześcigać się w szukaniu jak najbardziej żenującej muzyki. Żeby tym marmurowym cwaniakom zrzedły uśmiechy.
 
 Było po godzinach pracy, bawiliśmy się naprawdę dobrze, posmialiśmy się, pobujaliśmy na naszych obrotowych fotelach, ale było też dużo pracy i konktruktywnych rozmów o Javie, Cucumber, BDD, wzorcach projektowych,  uprzyjemniających kodowanie ficzerach InteliJ, zaczęliśmy budować solidnego DSL do szybszego i skuteczniejszego pisania scenariuszy testowych dla tego konkretnego projektu. To było niesamowite kreatywne i konstruktywne doświadczenie. Do tego stopnia, że pamiętam je doskonale pomimo upływu lat.
 
No i pamiętam jeszcze miny reszty zespołu nazajutrz, gdy na daily scrumie oznajmiłem, że wszystkie testy elegancko działają. Nikt nie uwierzył.

Nazwaliśmy to, co ze Stefanem odwaliliśmy "Sesją Wakawaka" na cześć naszej patronki.   
Tych szlagierów było więcej, niż dwa wymienione, ale pamiętam jak latałem na swoim krześle krzycząc "burn! burn! burn!". To było takie odświeżające.

Dla mnie był to fascynujący dowód na to, że w atmosferze raczej niekojarzoną z produktywnością udało nam się bardzo mocno ruszyć do przodu.

No i było o czym opowiadać innym ludziom w pracy, przy ekspresie do kawy.
 
## Jak to jest być specjalistą ?
Po calej tej historii usłyszałem od szefa, że w końcu na czymś zaczynam się znać, bo drążę temat, przerabiam go w projekcie i szukam rozwiązań. W końcu widać, że skupiam się na jednym temacie.   
No więc jakie to uczucie być specjalistą dla człowieka, który na żadnym temacie nie może się skupić na dłużej?
Nie wiem, bo nigdy szpecem w niczym nie byłem, ale dzięki jednej tylko sesji z kumplem to nie dość, że przeszła mi cała niechęć do tej konkretnej pracy, to jeszcze naprawdę polubiłem temat testów automatycznych. Wzrósł mój entuzjazm, nabrałem też dystansu, więc zacząłem więcej rzeczy w projekcie akceptować. Ludzi też zacząłem bardziej akceptować w ten jesienny, mroczny czas.    
Mój wewnętrzy Pan Jeż złożył kolce i poszedł sobie hibernować beze mnie.   
Byłem zwycięzcą.   
Byłem zwycięzcą.   
Byłem zwycięzcą.