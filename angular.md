---
id: angular
aliases: []
tags: []
---

# Angular CLI
Narzedzi ktore pozwala na latwe stworzenie projektu

npm install -g @angular/cli

Stworz nowy projekt
ng new <project-name>

Zainstalowac w VSC Angular Language Service i Angualar Essentials

Odpalanie projektu:
npm start


W root'cie projektu wszystkie pliki to sa konfiguracyjne

Te pliki odopowiadaja za to jak ts zostanie skompilowany do JSa (dziala z automatu)
- tsconfig.app.json
- tsconfig.json
- tsconfig.spec.json

Zarzadzaja zaleznosciami:
- package-lock.json
- package.json

Dodatkowe konfiguracje do angular cli i do tooli (raczej tu sie nic nie zminenia)
- angular.json

Zawiera reguly do stylizacji kodu:
- .editorconfig

Folder src

Najpierw ladowany jest html pozniej dolaczany jest ts (js)

W plikach podczas importu rozszerzenie jest nie potrzebne

Component tworzy HTML element. Component to decorator.

Na podstawie selector'a on wie jaki html generowac i do jakiego sie odwolac.
Componenty w Angularze to klasy ktore wykorzystuja dekorator @Component.

```
@Component({
    selector: 'app-header',
    standalone: true,
    templateUrl: './header.component.html',
    styleUrl: './header.component.css'
})
export class HeaderComponent {}
```


Aplikacja powinna byc budowana jako takie drzewo componentow. Jedna aplikacja = jedno drzewo ktorego rootem jest AppComponent.
Dzieki temu mozemy tylko raz wywolac bootstrapApplication z AppComponent. A pozniej nasze nowo stworzone komonenty wykorzystujemy w AppComponent.

Wtedy musimy jedynie wykorzystac pole ``import`` i upewnic sie ze wdanym componencie jest nasz nastepny komponent podany i wtedy mozemy wykorzystac go w html'u.

```typescript
import { HeaderComponent } from '../header/header.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HeaderComponent],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css',
})
export class AppComponent {}
```


Mozemy generowac nowe componenty z poziomu terminala:
``ng generate component <name>``

Wszystkie pola z Componentu sa dostepne w template'cie w html'u pozniej


W htmlu pozniej mozemy wykorzystywac np pola z Componentu przez "String interpolation" robimy to przez : {{ PRZEKAZYWANA_WARTOSC }}
Pozwala nam to na dostep do wszystkich pol ktore sa publiczne
Gdy nie podajemy zakresu to jest on public

Mozemy rowniez przekazywac wartosci przez property binding i wtedy atrybut musimy oznaczycz przez [] 

```html
<img src="{{ selectedUser.avatar }}" /> String interpolation
<img [src] = "selectedUser.avatar" /> Property binding
```


Mozemy zdefiniowac property jako metode z ktorej pozniej skorzystamy w templacie 
```typescript
get imagePath() {...}
```
Mozemy pozniej skorzystac z tej wartosci jak by byla zwyklym polem w classie

Robimy to dlatego ze chcemy miec czysty html a jak juz to jak najwiecej logiki w componentach.

Wyswietlanie wartosci dynamicznie to tylko jedna czesc na UI potrzebujemy rowniez nasluchiwac na input od usera.

Aby dodac eventListener musimy w danym elemencie podac nazwe eventu np "click" musimy podac ta wartosc w nawiasie zwyklym
```html
<button (click)="onSelectUser()">
</button>
```
Pozniej w Componencie musimy utworzyc ta metode onSelectUser

Jesli chcemy zmienic stan aplikacji (state) wystarczy zmienic nasze properites'y(pola) w klasie


Zone.js - odpowiada za detekcje tego ze zaszly zmiany w naszym componencie. On powiadamia angulara gdy np. wystopi user event lub jakis timer sie skonczy. Gdy user zrobi click np na jednym z componentow w lisciu to sprawdza on czy musi z update'owac pozostale (chyba przez cale drzewo)

Mamy dwa sposoby na update state'a 
- Opcja 1 wlasnie poleganie na zone.js i mechanizmu detekcji z angulara
- Opcja 2 Signals ktore powiadamiaja o zmianie danych angulara i wymagaja update'u UI 

Zeby skorzystac z sygnalow musimy zaimportowac signal z angular/core
```typescript
selectedUser = signal(DUMMY_USERS[randomIndex]);
```
Signal to kontener ktory zawiera wartosc. Angular zarzadza subskrypcjami do sygnalu zeby byc powiadomiony o zmianie stanu. Gdy ta zmiana wystapi to wtedy Angular wie jaka czesc UI powinien przeladowac.Zeby zmienic wartosc w signal musimy wywolac metode ``set()``

Aby zmienic w nim wartosc musimy wywolac ``selectedUser.set(VALUE)` `
Aby pobrac wartosc powinnismy skorzystac z wywolania ``selectedUser().name``  Ten read mowi ze probujemy pobrac ta wartosc w tym UI i on pod spodem tworzy subskrypcje ktora upewnia sie ze to miejsce w ktorym wywolany jest sygnal jest updateowane gdy ta wartosc sie zmieni.
Sygnaly zostaly wprowadzone od Angular 16 i pozwala na efektywniejsze przeladowywanie UI bez wykorzystania zone.js.

```typescript
  selectedUser = signal(DUMMY_USERS[randomIndex]);
  imagePath = computed(() => 'assets/users/' + this.selectedUser().avatar);
```

Jesli chcemy przekazac jakies dane do Componentu mozemy to zrobic z htmla ktory jest poziom wyzej i przekazac mu wartosc
``<app-user [avatar]="users[0].avatar" /> ``
To np robimy w app.component ale wtedy musimy sie upewnic ze nasz app.component.ts posiada informacje jaki to avatar i jest w stanie go przekazac

Pozniej ta wartosc musimy oznaczyc adnotacja @Input w Componencie


Jesli ts narzeka ze nasze property nie ma wartosci mozemy uzyc ! zeby poinformowac go ze ta wartosc bedzie wpisana i wtedy nie ma bledu np: `` @Input avatar!: string;``

Powinnismy korzystac z opcji `` @Input({required: true}) avatar!: string;`` zeby poinformowac ze to pole jest wymagane wtedy jesli ktos go nie poda to dostaniemy error w visual studio code.

To bylo zwykle podejscie a teraz z sygnalami.

Zamiast tego @Input() podajemy wartosc zmienna ``avatar = input<string>(TU_DEFAULTOWA_WARTOSC_JAK_NIE_TO_UNDEFINED);`` mozna zaznaczyc ze jest wymagany przez wywolanie funkcji `` input.required()`` wtedy nie mozna podac domyslnej wartosci bo ona powinna byc dodana wczesniej.
Z poza tego componentu wciaz korzystamy z tych inputow tak samo jakby byly zwyklymi wartosciami a nie sygnalami.
Jednak wtedy w html'u musimy wykorzystac do odczytania zwykle nawiasy np ``{{ name() }}`` i w naszym ts powinnismy wyliczyc wartosc w ``imagePath = computed(() => `assets/users/${this.avatar()}`);`` 
Dzieki temu ten imagePath bedzie przeliczany tylko wtedy gdy wartosc avatar sie zmieni.

Bo wczesniej przez get'a przeliczal sie za kazdym razem gdy cokolwiek sie stalo z naszym komponentem.

Te sygnaly ci przedstawilem sa readOnly ten z selectedUser nie ale ten z avatar tak. I jego wartosci nie da sie zmienic z poziomu ts.

Przez get nie dziala.

Nasz komponent moze rowniez nie tylko przyjmowac wartosci ale tez wysylac przy pomocy ``@Output()``
Mozemy to zrobic przez ``select = new EventEmitter<void>();`` Ta wartosc pozwoli nam zemitowac wartosc do komponentow ktore beda zainteresowane.

Wtedy w gore musimy nasluchiwac na te wartosci przez podanie np ``(select)="onSelectUser()"`` gdzie onSelectUser jest juz metoda w gornej czesci komponentow i pomaga zareagowac na emitowana wartosc w select.

```html
<li>
    <app-user [id]="users[1].id" [avatar]="users[1].avatar" 
        [name]="users[1].name" (select)="onSelectUser($event)" />
</li>
```

W ten sposob pobieramy wartosc wyemitowana z Output przez ten $event



Mozemy tez dodawac nasz output przez sygnaly z wykorzystaniem wlasnie funkcji ``select = output()``
Pozostala czesc zostaje taka sama, tutaj ta funkcja nie tworzy sygnalu tylko OutputEmitterRef. Dodali to po to zeby bylo krocej i zeby bylo spojnie z inputami pod wzgledem skladni.

