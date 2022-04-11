title: Behavior Driven React Native
author: Adam Dziendziel
tags:
  - Cucumber
  - BDD
  - ReactNative
  - DSP2017
  - Calabash
categories:
  - Tech
date: 2017-03-15 19:54:00
---
![](/images/03-title-image.jpg)

Dzisiaj kontynuuję temat living documentation. [Poprzednio](/Projektowanie-behawioralne) była bardziej “Specification” a dzisiaj będzię “Example”, bo zainstalujemy i skonfigurujemy środowisko do “ożywiania” specyfikacji. 


## Narzędzia

#### Cucumber
[Cucumber](https://cucumber.io/) jest to chyba najbadziej znany framework do uruchamiania testów behawioralnych (mój ulubiony pehapowy Behat jest mocno inspirowany ogórkiem). Został napisany w języku [Ruby](https://www.ruby-lang.org/pl/), więc musimy mieć w systemie interpreter tego języka.  
Najlepszym sposobem jego instalacji (polecanym mi przez kumpli mających już zeszlifowane ze starości rubinowe zęby) jest użycie [rvm (Ruby Version Manager)](https://rvm.io/rvm/install).   
Pozwala on na trzymanie w systemie różnych wersji Ruby oraz zestawów [gemów](https://en.wikipedia.org/wiki/RubyGems) i łatwego przełączania się między nimi, dzięki czemu nie ma problemu, gdy mamy różne projekty wymagające różnych wersji tych samych gemów.

__Instalacja Cucumber:__   
`$ gem install cucumber`

Swoją drogą node.js też ma taki swój version manager. [Zgadnijcie jak się nazywa](https://github.com/creationix/nvm) ;)



#### Calabash
Calabash jest frameworkiem do wykonywania Cucumberowych testów akceptacyjnych napisanych na Android oraz iOS. Ja w tym artykule skupię się tylko na tym pierwszym.

__Instalacja:__   
```bash
$ gem install calabash-android
$ cd path/to/NativeReport/android
$ calabash-adroid gen
```

Ostatnia komenda wygeneruje katalog __./features__ wraz z zawartością:
```
features
| support
| | app_installation_hooks.rb
| | app_life_cycle_hooks.rb
| | env.rb
| | hooks.rb
| step_definitions
| | calabash_steps.rb
| my_first.feature
```

Musimy wygenerować plik [.apk](https://pl.wikipedia.org/wiki/APK) (plik instalacyjny aplikacji androidowych)

1. Otwieramy Android Studio i otwieramy projekt. Ważne jest to, że musimy otworzyć podkatalog _android_ w katalogu naszej reactowej aplikacji, bo z punktu widzenia Android Studio to tutaj jest właściwa apka mobilna.
2. Wchodzimy do menu __Build__ i wybieramy __Build APK__
W efekcie plik zostanie zapisany w podkatalogu:    
_app/build/outputs/apk_

Aby ruszyły nam testy musimy jeszcze jednorazowo dokonać czegoś, co nazywa się _Resigning APK_:

`$ calabash-android resign app/build/outputs/apk/app-debug.apk`


#### Odpalamy pierwszy test
Hola, hola! Przede wszystkim musimy go jeszcze napisać :)   
W tym celu zmodyfikujmy wygenerowany ficzer _features/my_first.feature_

Zastąpmy istniejącą zawartość poniższą:
```gherkin
 Feature: Hello Feature
	Scenario: I want to see welcome text                         
	Then I see the text "Ogórek" 
```

Ten scenariusz sprawdzi, czy po uruchomieniu aplikacji wyświetla się napis "Ogórek".   
Aby test przeszedł musimy oczywiście zmodyfikować odpowiednio aplikację (_index.android.js_).

__Test start!__

`$ calabash-android run app/build/outputs/apk/app-debug.apk`

Powinniśmy zobaczyć jak w emulatorze nasza aplikacja jest uruchamiana a chwilę potem zamykana.

W konsoli natomiast dostaniemy informację, czy test się powiódł, lub informację dlaczego jednak nie.

![](/images/03-test-passed.jpg)


##### Słowo na zakończenie
Dlaczego taki wybór narzędzi?    
Swego czasu pracowałem jako tester, moim zadaniem było oprócz testów manualnych także pisanie i utrzymywanie testów automatycznych, które "stały" właśnie na Cucumber, ale w odmianie napisanej w java.    
Zacząłem dużo czytać, poznałem termin BDD, a później zacząłem kupować książki Gojko Adzica i sposób pisania scenariuszy testowych z użyciem gherkina bardzo wszedł mi w krew.   
Do tego stopnia, że często zgłaszam błędy używając (bez słów kluczowych) wzorca "given, when, then" :)

Reasumując: zdecydowały sentyment, nawyki i silna zajawka ideą _living documentation_.




__Linkografia:__  
[Tutorial konfiguracji Cucumber + Calabash](https://developer.xamarin.com/guides/testcloud/calabash/)   
[Oficjalna insrukcja instalacji Calabash](https://github.com/calabash/calabash-android/blob/master/documentation/installation.md)   
[Lista predefiniowanych stepów dla calabash-android](https://github.com/calabash/calabash-android/blob/master/ruby-gem/lib/calabash-android/canned_steps.md)