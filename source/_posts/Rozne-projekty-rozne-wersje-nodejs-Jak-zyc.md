title: 'Różne projekty, różne wersje nodejs. Jak żyć?'
author: Adam Dziendziel
tags:
  - Nodejs
  - zsh
categories:
  - Tech
date: 2017-07-11 12:41:00
---
Pracując ostatnio intensywnie "na frontendzie" mam projekty, które wymagają różnych wersji nodejs oraz, oczywiście, npm. Oczywiście główną przyczyną takiego stanu rzeczy jest data powstania projektu i oczywistą rzeczą wydaje się po prostu systematyczna aktualizacja zależności, ale życie rzadko kiedy bywa logiczne, nawet w branży w której dominują jednak umysły ścisłe.

## Bohater: nvm

Zacznijmy od tego, że instalowanie nodejs poprzez systemowe narzędzia do instalacji oprogramowania jest złym pomysłem, głównie ze względu na rzadsze aktualizacje tych pakietów. Tak więc, jeśli pracujesz na Ubuntu to __zapomnij__ o `$ apt-get install nodejs`.

O wiele lepszym rozwiązaniem jest użycie _Node Version Manager_, w praktyce nazywanego po prostu [nvm](https://github.com/creationix/nvm).

Pozwala on na instalowanie "obok siebie" różnych wersji nodejs i łatwo między nimi się przełączać.

Poniżej przestawię skróconą instrukcję użycia, a po więcej informacji odsyłam do dobrze napisanej, [oficjalnej dokumentacji](https://github.com/creationix/nvm#installation) narzędzia.

__Instalacja nvm:__
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```

__Lista dostępnych wersji nodejs:__
```
nvm ls-remote
```
__Instalacja wybranej wersji nodejs:__
```
nvm install 8.0.0
```
__Ustawienie konkretnej wersji nodejs jako domyślenej w systemie:__
```
nvm alias default 8.0.0
```
__Wyświetlenie wszystkich zainstalowanych wersji nodejs:__
```
nvm ls
```

W ten sposób możemy już w każdym momencie wybrać sobie wersję nodejs, jednak musimy to zrobić ręcznie i pamiętać o tym, że w danym projekcie musimy użyć jakieś starej wersji.    
A gdyby tak móc to zrobić automatycznie?

## Pomocnik bohatera: .nvmrc
Przede wszystkim należy dodać do projektu plik `.nvmrc` zawierający tylko jedną linijkę z wersją nodejs:
```
echo "8.0.0 > .nvmrc"
```
Teraz możemy już zapomnieć o wersji noda używanej w projekcie, ale wciąż musimy ją ustawić ręcznie wyknując komendę `nvm use`.

Aby wykonać powyższe polecenie automatycznie po wejściu do katalogu projektu (oczywiście mówię tutaj o wejściu do katalogu w konsoli) utwórzmy nowy plik `~/.zsh/auto-nvmrc`...

```bash
# place this after nvm initialization!
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```
... a następnie zaimportujmy w głównym pliku konfiguracyjnym powłoki `~/.zshrc`:
```
source "$HOME/.zsh/auto-nvmrc"       
```

I teraz mamy dwie świetne rzeczy:
- po __wejściu do katalogu__ zawierającego plik .nvmrc wywoływana jest komenda `nvm use`
- po __wyjściu z katalogu__ ustawiana jest wersja oznaczona jako domyślna.

## Nie tylko lokalnie
Powyżej zaprezentowane rozwiązanie świetnie sprawdza się na lokalnym środowisku deweloperskim, ale także na hostingach na których mamy dostęp do konsoli i możemy zainstalować nvm.

W poważniejszych projektach mamy zazwyczaj wszystko "skonteneryzowane", więc konfiguracja jest w pełni niezależna od systemu operacyjnego.