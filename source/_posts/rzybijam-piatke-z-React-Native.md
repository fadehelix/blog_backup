title: Przybijam piątkę z React Native
author: Adam Dziendziel
tags:
  - DSP2017
  - React
  - ReactNative
categories:
  - Tech
date: 2017-03-07 02:47:00
---
Przyszedł w moim życiu taki czas, że responsywne strony www to za mało, aby mieć poczucie że proponuję swoim klientom i współpracownikom rozwiązania adekwatne do ich potrzeb biznesowych.         

Świat aplikacji mobilnych jest dla mnie tak obcy jak dla typowego nerda świat paryskiej mody, więc czas na wybranie się w podróż ;)   
Jak ją zacząć? Najprostszy i najszybszy sposób to wpisanie w google “mobile app tutorial” i zdanie się na ranking wyszukiwarki ;) To jest dobre podejście, gdy nie mamy żadnych własnych preferencji i wymogów. Można w ten sposób odkryć fascynujące tematy.

Ja jednak lubię realizować możliwie wiele celów idąc jedną drogą, dlatego wymyśliłem sobie, że skoro od dłuższego czasu zabieram się za naukę react.js i mi to nie idzie, bo nie mam konkretnego projektu gdzie mógłbym ten framework wdrożyć, to podniosę poziom ekscytacji nauką i wejdę w dziewiczą puszczę zaznaczoną na mojej mapie jako “mobile app”.

Dlaczego React?
----------------
Nie czuję się programistą, o wiele bardziej lubię pracować z ludźmi, a najlepiej czuję się na froncie interakcji ludzi (tak, ludzi a nie “juserów”, to temat na innego posta) z interfejsami. Fascynuje mnie temat usability, stąd moją motywacją jest nauczenie się budowania interfejsów użytkownika, które sobie zaprojektuję. Komponentowa natura react jest też w zgodzie z tym co jest modne w świecie CSS (patrz: atomic design). 

Odpalmy tą furę
-------------------
A teraz do meritum, czyli wsiadam do autobusu relacji noob -  React Native.   
Na początku, aby sobie uprościć proces uczenia się, moje posty będą dotyczyć aplikacji na Androida rozwijanej na Ubuntu. Mój złoty "ksiomi" już się nie może doczekać ;)

Aby uruchomić w ogólę pierwszą testową apikację wykonuję krok po kroku [oficjalny tutorial](https://facebook.github.io/react-native/docs/getting-started.html#content).   
Ale, żeby nie było tak sterylnie, to kilka moich dodatkowych uwag:
Kilka moich uwag:

1. Aby mieć dostęp do komendy `react-native` należy dodać __sudo__ przed `npm install` - zmienia się wtedy lokalizacja instalacji pakieru na _/usr/local/lib_
2. Jeśli, tak jak ja, pracujesz na Kubuntu  i chcesz móc uruchamiać Android Studio z menu aplikacji, kliknij “prawą myszą” na ikonę KDE w pasku systemowym i wybierz “Edit application” a potem “Add item”. W polu command podaj ścieżkę do pliku wykonywalnego (np. _/opt/android-studio/bin/studio.sh_)
3. Sprawdź, czy masz zainstalowane w systemie __openjdk-8-jdk__
4. Procedura odpalania projektu:    
  * ~~Upewnij się, że najpierw uruchomiłeś emulator (polecenie `android avd`)~~   
  * ~~Następnie, w nowym oknie terminala, odpalamy serwer (?) poleceniem `react-native start`~~   
  * ~~I w końcu, w jeszcze innym oknie, komenda `react-native run-anddroid`~~   
  * ~~Uff… profit~~.
  
  __Aktualizacja pkt. 4__   
  Po zaktualizowaniu wersji SDK i samego Android Studio zobaczyłem taki oto komunikat próbując odpalić AVD w konsoli:
  ```bash
  The "android" command is deprecated.
For manual SDK, AVD, and project management, please use Android Studio.
For command-line tools, use tools/bin/sdkmanager and tools/bin/avdmanager
  ```
  
  Teraz można uruchomić projekt w Android Studio (mając zainstalowane pluginy _React Native Console_ oraz _React Native Tools_):
  1. Klikamy ikonkę __AVD Manager__ znajdującą się w głównym pasku narzędzi,
  2. Wybieramy, lub tworzymy emulator po czym zamykamy menedżera,
  3. W React Native Console klikamy __Start node server__ (zielony "przycisk play")
  4. W nowej sesji tegoż terminala (`ctrl + shift + T`) wpisujemy: `cd .. && react-native run-android`

Po kilkunastu sekundach powinna nam się w emulatorze pojawić aplikacja:
![](/images/01-emulator-first-run-app.jpeg)

Zepsujmy coś
------
Aby się upewnić, że wszystko działa jak należy edytujmy plik __index.android.js__ po czym edytujmy kod klasy NativeReport:
```javascript
export default class NativeReport extends Component {                                                                                                                                                                           
render() {                                                                                                                                                                                                                   
         return (                                                                                                                                                                                                                    
             <Text>Hello React Native!!!</Text>
        );
	}
}
```

Taaadaaaa!
![](/images/01-emulator-hello-react.jpeg)


Linkografia:
----------
[Zalety i wady React Native](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)