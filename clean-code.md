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
[[cdn]]
