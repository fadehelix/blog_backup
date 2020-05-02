title: Moje pierwsze małe Yo!
author: Adam Dziendziel
tags:
  - Tools
  - react
  - yo
  - npm
categories:
  - Tech
date: 2017-08-07 03:00:00
---
![Żródło: yo.posthang.com](/images/moje-pierwsze-yo-intro.png)
Czyli jak utworzyć prosty generator komponentu React.   
Dla uzupełnienia kontekstu polecam zobaczyć sobie kod juz gotowego generatora do którego link jest poniżej. 

{% githubCard user:fadehelix repo:generator-simple-react-component %}

## DRY
Don't Repeat Yourself, lubia powtarzać programiści. I mają rację, bo akurat w tej pracy zaletą jest to, że jeśli zidentyfikujemy jakąś czynność, którą często powtarzamy, to mamy masę narzędzi, które pozwalają nam ją zautomatyzować i skupić się na bardziej kreatywnej pracy.
Dzisiaj skupię się na jednym z nich, Yeoman, który postanowiłem zaprząc do generowania szkieletu komponentu, czyli piku .jsx (takie rozszerzenie zawsze nadaję plikowi zawierającemu komponent), oraz testu domyślnie tworzącego jedynie [snapshot](https://facebook.github.io/jest/docs/snapshot-testing.html) sprawdzający, czy komponent renderuje się poprawnie.

## Yo
Pierwszy raz tak na serio z Yeoman zetknąłem się przy [swoim pierwszym razie z Electron](/hotel-electron). Dzięki temu narzędziu jedną komendą mogłem utworzyć działający "boilerplate" apikacji co bardzo ułatwiło mi naukę, bo po wykonaniu zaledwie jednej komendy mogłem eksperymentować z kodem. 

Czas wrzucić odpowienie tło na słuchawki, pokazać środkowy palec konwenansom i jedziem z tworzeniem własnego generatora <3
{% youtube vmCJFFt2SV0 %}


### Szkielet generatora
Ten tekst opiera się na [oficjalnej dokumentacji](http://yeoman.io/authoring/index.html), więc nie jest to tutorial od A do Z, a raczej opis specyficznych dla mojego przypadku kroków, które poczyniłem.
Jednakże, gwoli kontekstu, podam kilka bardziej ogólnych informacji.

I tak najprostszy generator może wyglądać tak:
```javascript
module.exports = class extends Generator {
  constructor(args, opts) {
    super(args, opts);
  }

  prompting() {
    return this.prompt([{
      type: 'input',
      name: 'name',
      message: 'Your component name',
      default: this.appname
    }]).then(answers => {
      this.answers = answers;
    });
  }

  writing() {
    this.log('Here we can copy template');
  }
}
```
Funkcja `prompting` odpowiada za interakcję z użytkownikiem zadając mu pytania co do tworzonego komponentu. Powyżej użytkownik podaje jedynie nazwę.

Funckja `writting` odpowiada za przeniesienie i zmodyfikowanie plików szablonu komponentu. Docelowo zmieni ona nazwę szablonu na podaną przez użytkownika nazwę.

### Interakcja z użytkownikiem
W moim założeniu odpalając generator chcę móc ustawić jego nazwę i wybrać czy komponent będzie to bezstanowa funkcja, czy klasa.

Tak wygląda pełna funckja `prompting()`:
```javascript
 prompting() {
    return this.prompt([{
      type: 'input',
      name: 'name',
      message: 'Your component name',
      default: this.appname
    },
    {
      type: 'list',
      name: 'type',
      message: 'Component type',
      choices: ['Functional', 'Class']
    }
    ]).then(answers => {
      this.answers = answers;
    });
  }
```
A tak wyglądają powyższe opcje w konsoli po odpaleniu komendy `$ yo simple-react-component`:
![](/images/moje-pierwsze-yo-prompting.png)

### Szablon
Skoro dwa typy konponentu do wyboru, to potrzebuję dwóch szablonów. W każdym z nich chcę mieć wzór komponentu (plik .jsx) oraz podstawowy test (plik .test.js).
Tak prezentuje się struktura katalogu `templates`:
```bash
$ tree
.
├── MyClassComponent
│   ├── MyClassComponent.jsx
│   └── MyClassComponent.test.js
└── MyFunctionalComponent
    ├── MyFunctionalComponent.jsx
    └── MyFunctionalComponent.test.js
```

### Kopiowanie szablonu do docelowej lokalizacji
To już ostatni krok.
Utworzony przed chwilą szablon chcę teraz skopiować do lokalizacji, gdzie uruchomiłem generator.
Rozwijam więc funckję `writting()` o następujące instrukcje:

__Zmiana nazwy katalogu__
```javascript
this.fs.copy(
  this.templatePath('MyFunctionalComponent/'),
  this.destinationPath(this.answers.name)
)
```
I to było proste, wystarczyło podążać za oficjalną dokumentacją. Zderzyłem się jednak z dwoma problemami:

__Pierwszy bloker: Zmiana nazwy plików__   
Okazuje się, że na ratunek przychodzi... `gulp-rename`, czyli narzędzie do manipulacji plikami używane w Gulpie. Jest to możliwe, ponieważ zarówno Yeoman jak i Gulp wykorzystują obiekt [Vinyl](https://github.com/gulpjs/vinyl-fs) do obsługi plików. Bardzo się ucieszyłem, bo godziny spędzone na nauce Gulp okazały się być jeszcze lepszą inwestycją, niż sądziłem do tej pory.
```javascript
this.registerTransformStream(rename( function(path) {
  path.basename = path.basename.replace(/(MyFunctionalComponent)/g, that.answers.name)
}));
```

__Drugi bloker: Zmiana nazwy komponentu wewnątrz plików__   
Nawet nie uwieżysz o co ja tutaj pytałem google. W ktorymś momencie zacząłem wchodzić nawet w temat parserów i innej magii, która okazała się zbyteczna. Straciłem na tym ponad godzinę, a wystarczyło zatrzymać się dłużej i bardziej refleksyjnie przy problemie zmiany nazwy plików, aby tutaj rozwiązanie wyszło zza chmur, niczym pewna kometa jakieś 65 mln lat temu. Tą kometą, która zabiła mojego wewnętrznego dinozaura zwątpienia, okazało się być kolejne narzędzie z ekosystemu Gulp: `gulp-rename`.

```javascript
this.registerTransformStream(replace('MyFunctionalComponent', that.answers.name));
```
Widać z daleka, że ilość kodu akurat na zalogowanie ponad godziny pracy, prawda? PRAWDA!?

## Nikt nie ucieknie przed pisaniem testów
Ale, jak się okazało, może długo skutecznie próbować. Ostatnią godzinę spędziłem na próbie napisania testu sprawdzającego, czy generowane są odpowienie pliki komponentu i muszę przyznać, że dokumentacja jest dla mnie zbyt skąpa.    
Muszę się posiłkować testami napisanymi dla innych generatorów oraz analizą API biblioteki `yeoman-test`.   
Tak więc temat yo-testów zostanie opisany, ale dopiero w następnym te(k)ście.   
Tymczasem trzymaj za mnie kciuki, abym znów nie zabłądził w dokumentacji, a także zachęcam Cię do forkowania/gwiazdowania/zgłaszania projektu na Github:

{% githubCard user:fadehelix repo:generator-simple-react-component %}