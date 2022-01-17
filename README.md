# JNP1-2-maptel
Projekt robiony w parze.

Biblioteka standardowa języka C++ udostępnia bardzo przydatny typ
unordered_map. Jest to typ generyczny, pozwalający tworzyć słowniki
o różnych kluczach i wartościach, np. unordered_map<int, string>,
unordered_map<string, string>, a nawet
unordered_map<string, unordered_map<int, string>> i inne, jeszcze bardziej
złożone. Biblioteka standardowa języka C nie udostępnia podobnego typu.
W praktyce programistycznej często pojawia się też konieczność łączenia kodu
napisanego w językach C i C++.

Napisz w C++ moduł maptel udostępniający w języku C słowniki obsługujące zmiany
numerów telefonów. W języku C numer telefonu jest przechowywany w tablicy znaków
typu char jako ciąg maksymalnie 22 cyfr zapisanych w ASCII i jest zakończony
znakiem o wartości zero.

Moduł maptel powinien składać się z pliku nagłówkowego maptel.h deklarującego
jego interfejs oraz pliku maptel.cc zawierającego jego implementację.

Moduł maptel powinien udostępniać następujący interfejs:
```
  // Tworzy słownik i zwraca liczbę naturalną będącą jego identyfikatorem.
  unsigned long maptel_create(void);
```
```
  // Usuwa słownik o identyfikatorze id.
  void maptel_delete(unsigned long id)
```
```
  // Wstawia do słownika o identyfikatorze id informację o zmianie numeru
  // tel_src na numer tel_dst. Nadpisuje ewentualną istniejącą informację.
  void maptel_insert(unsigned long id, char const *tel_src, char const *tel_dst);
```
```
  // Jeśli w słowniku o identyfikatorze id jest informacja o zmianie numeru
  // tel_src, to ją usuwa. W przeciwnym przypadku nic nie robi.
  void maptel_erase(unsigned long id, char const *tel_src);
```
```
  // Sprawdza, czy w słowniku o identyfikatorze id jest zapisana zmiana numeru
  // tel_src. Podąża ciągiem kolejnych zmian. Zapisuje zmieniony numer w tel_dst.
  // Jeśli nie ma zmiany numeru lub zmiany tworzą cykl, to zapisuje w tel_dst
  // numer tel_src. Wartość len to rozmiar przydzielonej pamięci wskazywanej
  // przez tel_dst.
  void maptel_transform(unsigned long id, char const *tel_src, char *tel_dst, size_t len);
```

Nagłówek modułu maptel powinien udostępniać stałą TEL_NUM_MAX_LEN typu size_t
o wartości 22.

Ludzie bywają przewrotni i mając kod, który można używać w języku C, chcą go też
używać w C++. Należy zapewnić możliwość użycia pliku nagłówkowego maptel.h
w języku C++ w taki sposób, aby interfejs modułu maptel został umieszczony
w przestrzeni nazw jnp1 i nie był widoczny w globalnej przestrzeni nazw.

Moduł maptel powinien sprawdzać poprawność parametrów i poprawność wykonania
funkcji za pomocą asercji i wypisywać na standardowy strumień błędów informacje
diagnostyczne. Należy sprawdzać przynajmniej, czy identyfikator słownika jest
poprawny, czy przekazany wskaźnik nie jest NULL-em, czy przekazany napis nie
jest za długi, czy zawiera poprawne znaki i czy kończy się znakiem o wartości
zero. Kompilowanie z parametrem -DNDEBUG powinno wyłączać sprawdzanie
i wypisywanie.

Oczekiwane rozwiązanie powinno korzystać z kontenerów i funkcji udostępnianych
przez standardową bibliotekę C++. Nie należy definiować własnych struktur ani
klas. W szczególności nie należy przechowywać przekazanych przez użytkownika
wskaźników const char* bezpośrednio, bowiem użytkownik może po wykonaniu
operacji modyfikować dane pod uprzednio przekazanym wskaźnikiem lub zwolnić
pamięć. W rozwiązaniu nie należy nadużywać kompilacji warunkowej. Fragmenty
tekstu źródłowego realizujące wyspecyfikowane operacje modułu maptel nie powinny
zależeć od sposobu kompilowania - parametr -DNDEBUG lub jego brak (inaczej
wypisywanie informacji diagnostycznych nie miałoby sensu).
