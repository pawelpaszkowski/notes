---
id: clean-code
aliases: []
tags: []
---

# Znaczace nazwy
## Uzywaj nazw przedstawiajacych intencje
Nazwy powinny odzwierciedlac nasze zamiary. Powinnismy unikac nazw ktore sa nie oczywiste. Wybranie odpowiedniej nazwy to dobra inwestycja ktora pozniej pozwala nam osczedzic sporo czasu. Nazwa powinna informowac nas w jakim celu istnieje, co robi i jak jest uzywana. Jesli nazwa wymaga komentarza to znaczy ze nie ilustruje intencji.

- [!] ZLE NAZEWNICTWO
```java
for(int[] x : theList) {
    if(x[0] == 4) {
        list.add(x);
    }
}
```
- [x] DOBRE
```java
for(Cell cell : gameBoard) {
    if(cell.isFlagged()) {
        flaggedCells.add(cell);
    }
}
```
## Unikaj dezinformacji
- Bez skrotow
- Bez typow (np. accountList - po prostu accounts)
- Unikac nazw ktore niznacznie sie roznia np. `XYZControllerForEfficientHandlingOfStrings` i `XYZControllerForEfficientStorageOfStrings`

## Tworzenie wyraznych roznic
Nazwy typu class i klass, a1, a2, .. aN. Nie maja sensu. Nie stosowac slow typu variable, table, String w nazwach zmiennych. Stosowanie nazw typu Customer i CustomerInfo, Money i MoneyAmount sprawiaja ze te obiekty sa nieodroznialne i powoduja jedynie chaos.

## Tworzenie nazw ktore mozna wymowic
Bez nazw ktorych nie da sie wymowic np.
```java
Date genymdhms; // data generacji, rok, miesiac, dzien, godzina, minuta i sekunda.
Date generationTimestamp; // o wiele lepsze
```

## Korzystanie z nazw latwych do wyszukania
O wiele latwiej wyszukac `MAX_CLASSES_PER_STUDENT` niz liczbe 7 w calym kodzie.
## Przedrostki skladnikow
Nie ma potrzeby dodawac zadnych przedrostkow do nazw np. m_... LSB...
## Interfejsy i implementacje
Nie chcemy zeby uzytkownicy naszego kodu mysleli ze przekazywany jest interfejs zamiast implementacji. Wiec zamiast:
- `IShapeFactory` i `ShapeFactory`
lepsze juz jest:
- `ShapeFactory` i `ShapeFactoryImpl`

## Unikanie odwzorowania mentalnego
Nazwy powinny opisywac tym czym sa, zadnych skrotow czy niejasnych nazw.
Czytelnosc kodu jest wszystkim.
## Nazwy klas
Nazwa klasy powinna byc rzeczownikiem lub rzeczownikiem zlozonym. Przyklad dobrych nazw: `Invoice`, `UserController`, `EmailValidator`.
Zle: `ManageData` - brzmi jak metoda, `Processing` - brzmi jak proces a nie obiekt. `DataProcessor` - niby rzeczownik ale moze byc zbyt ogolny w zaleznosci od kontekstu.
## Nazwa metody
Metody nalezy opatrywac nazwami bedacymi czasownikami lub wyrazeniami czasownikowymi. Np. `postPayment`, `deletePage` lub `save`. 
Gdy konstruktory sa przeciazone nalezy uzywac metod fabryk o nazwach opisujacych argumenty.
```java
Complex fulcrumPoint = Complex.fromRealNumber(23.0);
```
jest zwykle lepsze od :
```java
Complex fulcrumPoint = new Complex(23.0);
```
Wtedy mozemy wymusic stosowanie tej praktyki przez ustawienie konstruktorow jako prywatnych.
## Nie badz dowcipny - nazwach metody i klas ogolnie w kodzie
## Wybieraj jedno slowo na pojecie
Nalezy wybierac jedno slowo na abstrakcyjne pojecie i trzymac sie tego. Na przyklad mylace jest stosowanie nazw `fetch`, `retrive` i `get` do analogicznych metod w roznych klasach. Podobane mylace jest wystepowanie nazw `Controller`, `Manager` oraz `Driver` w tej samej bazie kodu.
Jaka jest najwazniejsza roznica pomiedzy `DeviceManager` a `ProtocolController`?
Spojny leksykon jest ogromnym ulatwieniem dla programistow ktorzy musza korzystac z naszego kodu.
## Nie tworz kalamburow
Nalezy unikac uzywania tego samego slowa dla dwoch celow gdy mamy np metode `add` i dodaje ona dwie wartosci to nie powinnismy nazywac metody dodajacej element do kolekcji w ten sam sposob. Moze lepsza nazwa wtedy to `insert` lub `append`?
## Korzystanie z nazw dziedziny rozwiazania
Nalezy pamietac ze ludzie czytajacy nasz kod beda programistami. Mozna wiec korzystac z terminow informatycznych.
Nazwa `AccountVisitor` niesie ze soba wiele informacji dla kazdego programisty ktory zna wzorzec visitor.
Ktory programista nie bedzie wiedzial co to `JobQueue`?
Istnieje wiele technicznych zagadnien ktore programisci musza znac. Wybor nazwy techniczej jest zwykle najlepszym rozwiazaniem.
## Korzystanie z nazw dziedziny problemu
Wszedzie tam gdzie nie istnieje termin programistyczny dla wykonywanych operacji nalezy uzywac nazw z dziedziny problemu. W najgorszym przypadku programista ktory bedzie konserwowal nasz kod zapyta eksperta o znaczenie nazwy.
## Dodanie znaczacego kontekstu
Istnieje niewiele nazw, ktore same w sobie niosa wystarczajaco duzo tresci - w wiekszosci przypadkow tak nie jest. Z tego powdou konieczne jest umieszczenie nazw we wlasciwym kontekscie przez wstawienie ich w odpowiednio nazwane klasy, funkcje i przestrzenie nazw. Gdy wszystko inne zawiedzie, ostatnia deska ratunku moze byc zastosowanie przedrostka nazwy.

# Funkcje 
