title: Hotel Electron
author: Adam Dziendziel
tags:
  - Electron
  - Początek
  - Yo
categories:
  - Tech
date: 2017-06-05 13:59:00
---
![](/images/hotel-electron-intro.jpg)
Szybka notatka jak stworzyć super prostą (moją pierwszą!) aplikację desktopową z wykorzystaniem [Electron](https://electron.atom.io/).
Zadanie jakie sobie postawiłem, to z panelu [Hotel](https://github.com/typicode/hotel) uruchamianego w przeglądarce zrobić osobną aplikację desktopową,coby mieć faktyczny panel sterowania wszystkimi swoimi serwerami lokalnymi w każdej jednej aplikacji.   
W praktyce po prostu ładuję stronę "internetową" do okienka, czyli tworzę maksymalnie okrojoną z funkcji przeglądarkę. 

Oto, co powstało z tego śmiałego zamiaru: https://github.com/fadehelix/electro-hotel


Jeśli nazwa hotel w kotekście developmentu kojarzy Ci się tylko z miejscem, gdzie budzisz się skacowany podczas konferencji, to zapraszam do [posta o tym, co kryje się pod tą nazwą](/jest-hotel-jest-impreza).


### Plac zabaw: electron-quick-start

Przygodę z Electron rozpocząłem od [oficjalnego tutoriala](https://electron.atom.io/docs/tutorial/quick-start/) dla początkujących, w ramach którego dostajemy do zabawy prościutką aplikację. Wystarczy git clone i możemy eksperymentować na działającym projekcie.
```
# Clone the Quick Start repository
$ git clone https://github.com/electron/electron-quick-start

# Go into the repository
$ cd electron-quick-start

# Install the dependencies and run
$ npm install && npm start
```

## Moja pierwsza aplikacja

Chcąc sobie wypracować jakieś podejście na przyszłość poszukałem generatora szkieletu aplikacji Electron.    
Jeśli nie używałeś jeszcze generatora [Yeoman](http://yeoman.io/) to bardzo polecam go zainstalowac poleceniem `npm i -g yo`.

Instaluję generator aplikacji Electron: `npm i -g generator-electron`   
__!?__ Generatory Yeoman to narzędzie do szybkiego generowania szkieletów aplikacji lub modułów. Świetna implementacja [zasady DRY](http://programmer.97things.oreilly.com/wiki/index.php/Don%27t_Repeat_Yourself)  

Tworzę katalog projektu: `take electro-hotel`   
__!?__ _Komenda `take` jest to dostarczony w [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) alias na `mkdir electro-hotel && cd $_`   

Tworzę projekt: `yo electro-hotel`    
Dostałem w twarz trzema trudnymi pytaniami:
```
? What do you want to name your app? electro-hotel
? What is your GitHub username? fadehelix
? What is the URL of your website? http://fadehelix.github.io
```
Ok, zrobione. Mam szkielet aplikacji.

## Wsadzam Hotel do okienka

Jedyne co zrobiłem, aby to działało to, edytując plik `index.js`, podmieniłem ten kod:
```
win.loadURL(`file://${__dirname}/index.html`);
```
na ten:
```
win.loadURL(url.format({
	hostname: 'localhost',
	protocol: 'http:',
	port: '2000',
	slashes: true
}));
```

__!?__ Jeśli dostałeś błąd, że `url` jest niezdefiniowany to znaczy, że nie zaimportowałeś tego modułu i musisz dodać `const url = require('url');`

Tak prezentuje się owoc ostatniej godziny mojego życia:
![](/images/electro-hotel-screen-app-1.png)

__Uwaga!__ To nie była ostatnia godzina mojego życia w sensie absolutnym. Dalej żyję i działam. Mam też w planie rozwinąć tą aplikację, bo to całkiem niezłe labolatorium do nauki Electron, na to przyjdzie jeszcze czas. 

### Modyfikacja zachowania się linków.
Trochę problemów miałem z otwieraniem danej strony w przeglądarce (domyślnie linki otwierają docelowy adres w oknie aplikacji).   
Rozwiązaniem okazała się klasa `WebContents` dająca dostęp do zawartości `BrowserWindow`. Trochę to może mało eleganckie, ale po prostu wstrzyknąlem do załadowanego dokumentu java script przechwytujący kliknięcie i modyfikujący porządane zachowanie w odpowiedzi :
```
mainWindow.webContents.on('dom-ready', () => {
  mainWindow.webContents.executeJavaScript(`
    const shell = require('electron').shell;
    document.getElementById('app').addEventListener("click", (event) => {
      if(event.target.tagName === 'A') {
        event.preventDefault();					
        shell.openExternal(event.target.href);
      }
    });
  `);
});
```
Nie żebym był jakoś zadowolony z jakości tego rozwiązania, ale działa i nie zajęło mi dużo czasu. Niemniej jeśli będę projekt rozwijał i więcej czasu poświęcę Electron to postaram się to jakoś ładniej napisać.

Krótki czas na rozwiązanie + działa + jestem sam w tym projekcie = jestem zwycięzcą.

## Build
Generator dostarcza skonfigurowany packager uruchamamiany komendą `npm run build`. Wspomnianym "pekejdżerem" jest [electron-packager](https://www.christianengvall.se/electron-packager-tutorial/).    
Warto o tym wiedzieć, aby móc lepiej kontrolować buildy na różne systemy operacyjne.


__Taaadaaaaa!__ Mogę teraz mój świeży _Electro Hotel_ dodać do launchera.

Jeśli masz jakieś pomysły, pytania, uwagi to śmiało korzystaj z komentarzy poniżej.


## Bonus, czyli łyżka dziegciu: 
[Czy elektron do desktopowy Flash?](https://josephg.com/blog/electron-is-flash-for-the-desktop/) - Na artykuł o takim tytule natknąłem się szukając więcej informacji o Electron. Na pewno wart przeczytania.