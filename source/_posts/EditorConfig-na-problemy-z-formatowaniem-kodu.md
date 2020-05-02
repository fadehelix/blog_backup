title: EditorConfig na problemy z formatowaniem kodu
author: Adam Dziendziel
tags:
  - Zespół
  - Dobre praktyki
  - Javascript
categories:
  - Tech
date: 2017-09-01 15:25:00
---
![](/images/editorconfig-intro.jpeg)

Jednym z najczęstszych i irytujących problemów w zespole jest formatowanie kodu. 
Nie jest to takie proste do ogarnięcia ponieważ zazwyczaj mamy do czynienia z różnymi językami (np. javascript, php i html) oraz indywidualnymi upodobaniami poszczególnych programistów.

## Dlaczego należy zwracać uwagę na formatowanie kodu?

Przede wszystkim jeśli ktoś nie formatuje odpowiednio kodu to zmiejsza to jego (tego kodu) czytelność. Zamiast koncentrować się na logice to osoba czytająca jest rozpraszana przez "bałagan". To jest ważne, bo większość dobrych programistów to jednak osoby mocno zwracające uwagę na detale.    

Jednak najczęstszy przypadek to sytuacja w której twoje zmiany zawierają się w zaledwie paru linijkach w jednym pliku. Jeśli zrobisz `git log` to widzisz dokładnie te zmiany. Teraz wyobraź sobie, że na końcu zrobiłeś "reformat" całego kodu (bo tak jest najprościej - w Webstorm to jest po prostu `Ctrl + Alt + L`) i znów robisz `git log`. Co widzisz? Nic. Nie widzisz jakich konkretnie zmian dokonałeś ponieważ, w zależności od tego co zrobił reformat, masz masę czerwieni.    
Ta sytuacja dotyczy też Pull/Merge Requesta w repozytorium, tylko tutaj już wkurwiamy tego, kto dokonuje review. Gratulacje.

I teraz z mojego doświadczenia wynika, że każdy w zespole ma swoje upodobania co do formatowania (taby zamiast spacji, a jak spacje to cztery a nie dwie, klamry w funkcjach w nowej linii, parametry funkcji ze spacjami pomiędzy nimi a nawiasem...).   
Jeśli nawet mamy w zespole ustalone zasady formatowania, to zawsze ktoś może coś eksperymentować, albo do projektu wchodzi nowa osoba. Zamiast poświęcić czas na dyskusje o rozwiązywaniu problemów biznesowych to ktoś marnuje zasoby na poprawianie wcięć i połapanie się co zostało w ogóle zrobione w tym commicie.


## EditorConfig przybywa z odsieczą
Spotkałem się z różnymi rozwiązaniami wymuszenia - tak, wiem że to brzydkie słowo, ale jest takie angielskie określenie często pojawiające się na github: _opinionated_ które można tłumaczyć jako "uparty" i uważam, że większość programistów to są żywe chodzące tego słowa - jednolitego formatowania kodu niezależnie od języka. Dochodzi jeszcze problem komunikacji, bo jakoś tak się śmiesznie składa, że w IT komunikacja to często jest trochę taki mityczny jednorożec pasący się na zielonych łąkach Atlantydy. No, w każdym razie nie jest to takie proste zrobić, aby każdy w zespole sobie identycznie edytor skonfigurował.

Całe szczęście na pokręconych ścieżkach życia można też spotkać mądrych i pragmatycznych ludzi, którzy potrafią podsunąć świetne i proste w implementacji rozwiązania. I tak razu pewnego [Piotrek](https://twitter.com/sobi3ch) wrzucił na naszego RatioWebowego ~~slacka~~ mattermosta propozycję użycia w projektach [EditorConfig](http://editorconfig.org/) w celu ujednolicenia formatowania kodu we wszystkich projektach przez wszystkich developerów.  
Przyznam, że na początku byłem sceptyczny no bo przecież mamy te wszystkie lintery automatycznie odpalane przez Gulp, a EditorConfig w [niektórych edytorach wymaga zainstalowania pluginu](http://editorconfig.org/#download).

Oto przykładowa konfiguracja wzięta ze strony projektu:
```
# EditorConfig is awesome: http://EditorConfig.org

# top-most EditorConfig file
root = true

# Unix-style newlines with a newline ending every file
[*]
end_of_line = lf
insert_final_newline = true

# Matches multiple files with brace expansion notation
# Set default charset
[*.{js,py}]
charset = utf-8

# 4 space indentation
[*.py]
indent_style = space
indent_size = 4

# Tab indentation (no size specified)
[Makefile]
indent_style = tab

# Indentation override for all JS under lib directory
[lib/**.js]
indent_style = space
indent_size = 2

# Matches the exact files either package.json or .travis.yml
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```


### Zalety
* Działa z dowolnym językiem
* Możemy ustalić inne zasady dla każdego języka
* Konfiguracja w osobnym pliku (czyli jest w repozytorium) dzięki czemu jeśli ktoś coś zmieni to wiemy kto to zrobił, a zmiana formatowania zajdzie u wszystkich
* Zakładając, że nasz edytor ma włączoną obsługę EditorConfig, formatowanie odbywa się transparentnie dla developera


## A może by tak jednak linter?
Lintery są swietne, bo poza formatowaniem kodu potrafią też znajdywać nieużywane zmienne, "puste" importy, analizować scope zmiennych itd. Jednak o ile świetnie działają w CSS/SASS oraz javascript to już nie wiem czy tak dobrze sobie radzą np. z PHP. Poza tym są to raczej "kombajny" co powoduje, że możemy mieć pokusę je zmieniać, bo znaleźliśmy lepszy ( ja tak porzuciłem [eslint](https://eslint.org/) na rzecz jego "pocukrowanej" odmiany [XO](https://github.com/sindresorhus/xo).  A my tutaj chcemy tylko kontrolować formatowanie kodu.   
Uważam po prostu, że lepiej używać więcej prostych narzędzi, niż kilka złożonych, niby wielofunkcyjnych.