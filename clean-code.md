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
## Male funkcje
Funkcje powinny miec nie wiecej niz 20 wierszy
## Bloki i wciecia
Funkcja nie moze byc na tyle duza, aby zawierala zagniezdzone struktury. Dlatego poziom wciec w funkcji nie powinien przekraczac dwoch. Dzieki temu funkcje sa czytelniejsze i bardziej zrozumiale.
## Wykonuj jedna czynnosc
> FUNKCJE POWINNY WYKONYWAC JEDNA OPERACJE, POWINNY ROBIC TO DOBRZE. POWINNY ROBIC TYLKO TO.
np.
```java
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception{
    if(isTestPage(pageData)){
        includeSetupAndTeardownsPages(pageData, isSuite);
    }
    return pagaData.getHtml();
}
```

W przypadku tej porady ciezko powiedziec co to jest "jedna operacja". Czy ten kod wykonuje jedna operacje? Latwo pokazac ze sa to 3 czynnosci:
1. Sprawdzenie czy strona jest testowa
2. Jezeli tak, dolaczenie stron konfiguracyjnych i rozbioru
3. Wygenerowanie strony w HTML-u.

Nalezy zwrocic uwage ze te trzy kroki z funkcji znajduja sie o jeden poziom abstrakcji ponizej zadeklarowanego przez nazwe funkcji.
Jezeli funkcja wykonuje tylko operacje znajdujace sie o jeden poziom ponizej zadeklarowanej nazwy funkcji to wykonuje ona jedna operacje, W koncu powodem pisania funkcji jest dekompozycja duzych zagadnien(inaczej mowiac nazwy funkcji) na zbior operacji znajdujacych sie na nizszych poziomach abstrakcji.
Jednym ze sposobow sprawdzenia czy funkcja wykonuje tylko "jedna operacje" jest proba wyodrebnienia z niej innej funkcji, ktora nie jest tylko reoorganizacja jej implementacji.

## Sekcje wewnatrz funkcji
Jezeli funkcja jest podzielona na sekcje jak deklaracja, inicjalizacja oraz sito. to oczywisty symptopm wykonywania wiecej niz jednej operacji.(W tym przypadku byl to spora metoda w ktorej sekcje sa kodem a nie odrebnymi metodami jesli bylyby to metody to byloby ok.. (chyba))

## Jeden poziom abstrakcji w funkcji
np 
- wysoki poziom absrakcji ```getHTML()```
- sredni poziom absrakcji ```String pagePathName = PathParser.render(pagePath);```
- niski poziom abstrakcji ```append("\n");```

Mieszanie poziomow abstrakcji w jeden funkcji jest zawsze mylace. Czytelnicy moge miec problemy z rozpoznaniem czy okreslone wyrazenie jest waznym zagadnieniem czy malo istotnym szczegolem. Co gorsze, gdy szczegoly wymieszaja sie z waznymi koncepcjami, rodzi sie pokusa do dawania do funkcji coraz wiekszej liczby szczegolow.

## Czytanie kodu od gory do dolu - zasada zstepujaca
Chcemy aby kod mozna bylo czytac od gory do dolu. Chcemy, aby po kazdej funkcji znajdowala sie kolejna, na nastepnym poziomie abstrakcji, dzieki czemu mozna czytac program, schodzac o jeden poziom abstrakcji nizej wraz z przejsciem do kolejnej funkcji w pliku. Nazywa sie to zasada zstepujaca.

## Instrukcje switch
Czasami tworzymy metody typu ```calculatePay(Employee e)``` ktore na podstawie danego employee przelicza platnosc. Moze taka metoda powinna znajdowac sie w klasie Employee okreslonego typu np HourlyEmployee i byc stworzona przez fabryke abstrakcyjna przez co kazdy employee bedzie mial ta wartosc osobno wyliczone oczywisce switch bedzie w naszym przypadku dalej wystepowal ale bedzie on na poziomie tworzenia pracownika a nie samej metody. Pomoze nam to pozniej nie powielac tych switchow na poziomie innych metod typu ```deliveryPay(Money money)```. W ktorych podobny switch by sie znajdowal. Teraz kazda metoda bedzie miec osobna implementacje w odpowiednim typie.
## Korzystanie z nazw opisowych
> Wiemy ze pracujemy na czystym kodzie, jezeli kazda procedura okazuje sie taka, jakiej sie spodziewalismy
Polowa sukcesu w osiagnieciu tego stanu jest wybor dobrych nazw dla malych funkcji wykonujacych jedna operacje. Im mniejsze i lepiej ukierunkowane sa funkcje tym latwiej jest wybrac dla nich opisowa nazwe.

Nie nalezy obawiac sie konstruowania dlugich nazw. Dluga opisowa nazwa jest lepsza niz krotka enigmatyczna.
## Argumenty funkcji
Idealna liczba argumentow dla funkcji jest zero. Nastepnie mamy jeden i dwa. Nalezy unikac konstruowania funkcji o trzech argumentach.

Argumenty sa klopotliwe. Wymagaja one uzycia sporo enegii koncepcyjnej. Moze lepiej sprobowac schowac argumenty jako pola danej klasy. I wtedy dzialanie bedzie duzo bardziej przejrzyste. Argumenty sa duzo bardziej klopotliwe z punktu widzenia testowania. Trudno napisac wszystkie testy jednostkowe zapewniajace ze wszystki kombinacje argumentow beda dzialaly prawidlowo. (Nie do konca tak jest bo i tak trzeba wiele przypadkow pewnie przetestowac na podstawie inicjalizacji obiektu a nie w wywolaniu funkcji).
Argumenty wyjsciowe sa trudniejsze do zrozumienia niz argumenty wejsciowe. Gdy czytamy funkcje zwykle zakladamy ze dane wchodza do funkcji i wychodzia z funkcji poprzez zwracana wartosc. Zwykle nie oczekujemy ze dane beda wychodzily z funkcji przez argumenty. (Chodzi o fakt zmiany stanu obiektu po wywolaniu funkcji bardziej przejrzyste moze sie okazac gdy to stan obiektu zmienimy).

## Czesto stosowane funkcje jednoargumentowe
Istnieja dwa czesto spotykane powody przekazania jednego argumentu funkcji.
- Mozemy zadawac pytanie na temat tego argumentu ```boolean fileExists("MyFile.txt");```
- Mozemy operowac na argumencie, przeksztalcac go w cos innego i zwracac wynik. ```InputStream fileOpen("NazwaPliku);```

Rzadziej wystepuja zdarzenia - wykorzystywany argument jest do zmiany stanu systemu np ```void passwordAttemptFailedNTimes(int attempts);```
    Nalezy unikac funkcji ktore nie naleza do zadnej z tych postaci. Np. nie uzywac argumentu wyjsciowego dla transformacji
- [!] ```void transform(StringBuffer out)```
- [x] ```StringBuffer transform(StringBuffer in)```

## Argumenty znacznikowe (boolean)
Argumenty znacznikowe sa brzydkie. Przekazanie wartosci boolean do funkcji jest naprawde niepraktyczne. Od razu komplikuje to sygnature metody, wyraznie informujac, ze funkcja wykonuje wiecej niz jedna operacje. Wykonuje jedna operacje jezeli znacznik jest true i inna gdy false.

## Funkcje dwuargumentowe




