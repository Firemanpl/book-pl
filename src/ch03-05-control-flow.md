## Kontrola Przepływu
Podejmowanie decyzji o uruchomieniu kodu w zależności od tego, czy warunek w funkcji jest prawdziwy oraz wielokrotnym uruchamianiu kodu, gdy warunek jest prawdziwy w większości języków są bloki konstrukcyjne. Najpopularniejszymi konstrukcjami, które pozwalają kontrolować przepływ wykonywania kodu Rust są wyrażenia `if` oraz pętle.

### Wyrażenia `if`
Wyrażenia `if` pozwalają na rozgałęzienie kodu w zależności od panujących warunków. Podajemy warunek, następnie wyrażamy: "Jesli ten warunek jest spełniony, uruchom ten blok kodu. Jeśli warunek nie jest spełniony nie uruchamiaj go."

Stwórz nowy projekt i nazwij go *galezie* w twoim katalogu *projects* w celu zbadania wyrażenia `if`. W pliku *src/main.rs* wprowadź następujące dane: 

<span class="filename">Plik: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-26-if-true/src/main.rs}}
```
Wszystkie wyrażenia `if` zaczynają się od słowa kluczowego `if`, po którym następuje warunek. W tym przypasku warunek sprawdza czy zmienna `number` ma wartość mniejszą niż 5. Blok kodu, który chcemy wykonać, jeśli warunek jest prawdziwy, jest umieszczony zaraaz po warunku wewnątrz nawiasów klamrowych. Bloki kodu związane z warunkami w wyrażeniach `if` są
czasami nazywane *arms*, podobnie jak ramiona w wyrażeniach `match`, które omawialiśmy w rozdziale [“Porównanie Gościa do tajnego numeru”][comparing-the-guess-to-the-secret-number]<!-- ignore --> sekcja Rozdział 2.

Opcjonalnie możemy również dołączyć wyrażenie `else`, aby dać programowi alternatywny blok kodu do wykonania pod warunkiem, że zostanie oceniony jako fałszywy. Jeśli nie podamy wyrażenia `else` oraz warunek jest fałszywy, program po prostu pominie blok `if` i przejdzie
do następnego fragmentu kodu.


Spróbuj uruchomić ten kod; Na wyjściu powinieneś zobaczyć następujący wynik: 

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-26-if-true/output.txt}}
```

Spróbujmy zmienić wartość `liczby` na wartość, która sprawia, że warunek.
`false`, aby zobaczyć co się stanie:

```rust,ignore
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-27-if-false/src/main.rs:here}}
```

Uruchom program ponownie, oraz spójrz na wynik:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-27-if-false/output.txt}}
```

Warto też zauważyć, że warunek w tym kodzie *musi* być `bool`-em. Jeśli
warunek nie jest `bool`-em, otrzymamy błąd. Na przykład, spróbuj uruchomić
następujący kod:

<span class="filename">Plik: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/src/main.rs}}
```

Tym razem warunek `if` ma wartość 3 i rust zwaca błąd:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/output.txt}}
```

Błąd wskazuje, że Rust oczekiwał wartości „bool”, ale otrzymał liczbę całkowitą. w odróżnieniu od języków Ruby oraz JavaScript, Rust nie będzie automatycznie próbował konwertować innych typów na `bool`-a. Musisz być wyraźny i zawsze dostarczać `if` z wartością logiczną jako jego warunek. Jeśli chcemy, aby blok kodu `if` był uruchamiany tylko wtedy, gdy liczba nie jest równa `0`, na przykład: Możemy zamienić wyrażenie `if` na poniższe:

<span class="filename">Plik: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-29-if-not-equal-0/src/main.rs}}
```

Uruchomienie tego kodu spowoduje wyprintowanie: `number wynosi coś innego niż zero`.

#### Obsługa wielu warunków za pomocą `else if`

Możesz mieć wiele warunków z kombinacją `if` oraz `else`. Na przykład:

<span class="filename">Plik: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-30-else-if/src/main.rs}}
```

Ten program ma cztery możliwe ścieżki, którymi może podążać. Po uruchomieniu powinieneś zobaczyć następujące dane wyjściowe:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-30-else-if/output.txt}}
```

Kiedy program się uruchomi, sprawdzi każdy warunek `if` oraz wykona pierwszą treść warunku dla której jest spełniony.Zauważ, że mimo iż 6 jest podzielne przez 2, nie widzimy wyniku: `number jest podzielny przez 2`, oraz `number nie jest podzielny przez 4, 3, ani 2` tekstu z bloku `else`. Dzieje się tak ponieważ Rust wykonuje tylko blok kodu tylko dla pierwszego prawdziwego warunku, lub dla pierwszego, kiedy już go znajdzie nie sprawdza nawet tych pozostałych.

Używając za wiele wyrażeń `else if` może i z pewnością będzie zaśmiecało twój kod. Więc jeśli masz więcej niż jedno takie wyrażenie możesz chcieć zrefaktoryzowac swój kod w celu poprawienia jego czytelności. Rozdział 6 opisuje jak wydajne konstruowanie branch-ów zwane `match` dla tych zagadnień.

#### Użycie `if` w intrukcji stanu `let`

Ponieważ `if` jest wyrażeniem, możemy go użyć po prawej stronie instrukcji `let`, jak na listingu 3.2.

<span class="filename">Plik: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-02/src/main.rs}}
```

<span class="caption">Listing 3-2: Przypisanie wyniku wyrażenia `if` do zmiennej</span>

Zmienna `number` będzie powiązana z wartością opartą na wyniku wyrażenia `if`. Uruchom ten kod, aby zobaczyć co się stanie:

```console
{{#include ../listings/ch03-common-programming-concepts/listing-03-02/output.txt}}
```
Pamiętaj, że bloki kodu oceniają ostatnie wyrażenie w nich zawarte, oraz liczby same w sobie również są wyrażeniami. W tym przypadku, wartość całego wyrażenia `if` zależy od tego, który blok kodu zostanie wykonany. Oznacza to, że wartości, które mogą być wynikami każdego z ramion wyrażenia `if` muszą być tego samego typu; na Listingu 3-2, wynikami zarówno ramienia `if` jak i `else` były liczby całkowite `i32`.Jeśli typy są niedopasowane, jak w następującym przykładzie, otrzymamy błąd:

<span class="filename">Plik: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/src/main.rs}}
```

Gdy spróbujemy skompilować ten kod, otrzymamy błąd. Ramiona `if` i `else`
mają typy wartości, które są niekompatybilne, a Rust wskazuje dokładnie gdzie
znaleźć ten problem w programie:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/output.txt}}
```

Wyrażenie w bloku `if` daje w wyniku liczbę całkowitą, a wyrażenie w bloku `else` daje w wyniku łańcuch. To nie zadziała, ponieważ zmienne muszą mieć jeden typ. Rust musi wiedzieć w czasie kompilacji, jakiego typu jest zmienna numeryczna, aby mógł zweryfikować w czasie kompilacji, czy jej typ jest poprawny wszędzie tam, gdzie używamy `number`. Rust nie byłby w stanie tego zrobić, gdyby typ `number` był określany tylko w czasie wykonywania; kompilator byłby bardziej złożony i dawałby mniej gwarancji dotyczących kodu, gdyby musiał śledzić wiele hipotetycznych typów dla dowolnej zmiennej.

### Powtórzenie z Pętlami

Często przydatne jest wykonanie bloku kodu więcej niż raz. Do tego zadania Rust udostępnia kilka *loops*. Pętla przechodzi przez kod wewnątrz ciała pętli do końca, a następnie zaczyna się natychmiast od samego początku. To experiment with loops, let’s make a new project called *petle*.

Rust has three kinds of loops: `loop`, `while`, and `for`. Let’s try each one.

#### Powtarzający sie kod `loop`

Słowo kluczowe `loop` mówi Rustowi, aby wykonywał blok kodu w kółko w nieskończoność lub do momentu, gdy wyraźnie każesz mu przestać.

Jako przykład zmieńmy plik *src/main.rs* w twoim katalogu *petle* aby wyglądał następująco:

<span class="filename">Plik: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-32-loop/src/main.rs}}
```

Kiedy uruchomimy program, zobaczymy na wyjściu `znowu!` drukowane w kółko, dopóki nie zatrzymamy programu ręcznie. Większość terminali obsługuje skrót klawiaturowy, <span class="keystroke">ctrl-c</span>, w celu przerwania programu, który utknął w ciągłej pętli. Spróbuj:

<!-- manual-regeneration
cd listings/ch03-common-programming-concepts/no-listing-32-loop
cargo run
CTRL-C
-->

```console
$ cargo run
   Compiling petle v0.1.0 (file:///projects/petle)
    Finished dev [unoptimized + debuginfo] target(s) in 0.29s
     Running `target/debug/petle`
znowu!
znowu!
znowu!
znowu!
^Cznowu!
```

Symbol `^C` reprezentuje miejsce, w którym nacisnąłeś span class="keystroke">ctrl-c
</span> . Możesz zobaczyć to słowo ponownie lub nie! drukowane po `^C`, w zależności od tego, gdzie kod był w pętli, kiedy otrzymał sygnał przerwania.

Na szczęście Rust zapewnia inny, bardziej niezawodny sposób na wyrwanie się z pętli. Możesz umieścić słowo kluczowe `break` w pętli, aby powiedzieć programowi, kiedy ma przestać wykonywać pętlę.Przypomnijmy sobie, że zrobiliśmy to w grze w zgadywanie w sekcji [“Quitting After a Correct Guess”][quitting-after-a-correct-guess]<!-- ignore--> w rozdziale 2, aby wyjść z programu, gdy użytkownik wygrał grę, odgadując prawidłową liczbę.

#### Zwracanie wartości z pętli

Jednym z zastosowań `loop` jest ponowienie operacji, o której wiesz, że może się nie powieść, na przykład sprawdzenie, czy wątek zakończył swoje zadanie. Jednak może być konieczne przekazanie wyniku tej operacji do reszty kodu.
One of the uses of a `loop` is to retry an operation you know might fail, such
as checking whether a thread has completed its job. However, you might need to
pass the result of that operation to the rest of your code. Aby to zrobić, możesz dodać wartość, którą chcesz zwrócić po wyrażeniu `break` używanym do zatrzymania pętli; ta wartość zostanie zwrócona z pętli, abyś mógł jej użyć, jak pokazano tutaj:

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-33-return-value-from-loop/src/main.rs}}
```

Przed pętlą deklarujemy zmienną o nazwie `counter` i inicjalizujemy ją na `0`. Następnie deklarujemy zmienną o nazwie `result`, która będzie przechowywać wartość zwróconą z pętli. W każdej iteracji pętli dodajemy `1` do zmiennej `counter`, a następnie sprawdzamy, czy licznik jest równy `10`. Kiedy tak jest, używamy słowa kluczowego `break` z licznikiem `wartości * 2`. Po pętli używamy średnika, aby zakończyć instrukcję, która przypisuje wartość do `result`. Na koniec drukujemy wartość w `result`, która w tym przypadku wynosi 20.

#### Pętle warunkowe z `while`

Często przydatne jest dla programu oszacowanie warunku w pętli. Dopóki warunek jest prawdziwy, pętla działa. Gdy warunek przestaje być prawdziwy, program wywołuje `break`, zatrzymując pętlę. Ten typ pętli można zaimplementować za pomocą kombinacji `loop`, `if`, `else` i `break`; Możesz spróbować tego teraz w programie, jeśli chcesz.

Jednak ten wzorzec jest tak powszechny, że Rust ma dla niego wbudowaną konstrukcję językową, zwaną pętlą `while`. Listing 3-3 używa `while`: program zapętla się trzy razy, za każdym razem odliczając w dół. Następnie po wykonaniu pętli wypisuje kolejną wiadomość oraz kończy działanie.

<span class="filename">Plik: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-03/src/main.rs}}
```

<span class="caption">Listing 3-3: Użycie pętli while do uruchomienia kodu, gdy warunek jest spełniony</span>

Ta konstrukcja eliminuje wiele zagnieżdżeń, które byłyby konieczne, gdybyś użył `loop`, `if`, `else` i `break`. Gdy warunek jest spełniony, kod działa; w przeciwnym razie wychodzi z pętli.

#### Zapętlanie kolekcji za pomocą pętli `for`

Możesz użyć konstrukcji `while`, aby przejść przez elementy kolekcji, takie jak tablica. Na przykład spójrzmy na Listing 3-4.

<span class="filename">Plik: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-04/src/main.rs}}
```

<span class="caption">Listing 3-4: Przechodzenie przez każdy element kolekcji za pomocą pętli `while`</span>

Tutaj kod liczy elementy w tablicy. Zaczyna się od indeksu `0`, a następnie zapętla się, aż osiągnie ostatni indeks w tablicy (gdy `index < 5` nie jest już prawdziwy). Uruchomienie tego kodu spowoduje wydrukowanie każdego elementu w tablicy:


```text
{{#include ../listings/ch03-common-programming-concepts/listing-03-04/output.txt}}
```

Zgodnie z oczekiwaniami wszystkie pięć wartości tablicy pojawia się w terminalu. Mimo że `index` osiągnie w pewnym momencie wartość `5`, pętla zatrzymuje się przed próbą pobrania szóstej wartości z tablicy.

Ale to podejście jest podatne na błędy; Możemy spowodować panikę programu, jeśli długość indeksu jest nieprawidłowa. Jest również powolny proces, ponieważ kompilator dodaje kod wykonawczy, aby wykonać warunkowe sprawdzenie każdego elementu w każdej iteracji pętli.

Jako bardziej zwięzłą alternatywę możesz użyć pętli `for` i wykonać kod dla każdego elementu w kolekcji. Pętla `for` wygląda jak kod z listingu 3-5.

<span class="filename">Plik: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-05/src/main.rs}}
```

<span class="caption">Listing 3-5: Przechodzenie przez każdy element kolekcji za pomocą pętli `for`</span>

Gdy uruchomimy ten kod, zobaczymy ten sam wynik, co na listingu 3-4. Co ważniejsze, zwiększyliśmy teraz bezpieczeństwo kodu i wyeliminowaliśmy ryzyko wystąpienia błędów, które mogą wynikać z wyjścia poza koniec tablicy lub niedostatecznego posunięcia się i pominięcia niektórych elementów.

Na przykład w kodzie z Listingu 3-4, jeśli zmieniłeś definicję tablicy `a` tak, aby miała cztery elementy, ale zapomniałeś zaktualizować warunek do while `index < 4`, program zwrócił by panic. Używając pętli `for`, nie będziesz musiał pamiętać o zmianie żadnego innego kodu, jeśli zmienisz liczbę wartości w tablicy.

Bezpieczeństwo i zwięzłość pętli for sprawiają, że są one najczęściej używaną konstrukcją pętli w Rust. Nawet w sytuacjach, w których chcesz uruchomić jakiś kod określoną liczbę razy, jak w przykładzie z odliczaniem, w którym wykorzystano pętlę `while` z listingu 3-3, większość Rust-owców użyliby pętli `for`. Sposobem na to byłoby użycie `Range`, który jest typem zapewnianym przez standardową bibliotekę, która generuje wszystkie liczby w sekwencji, zaczynając od jednego numeru i kończąc na innym.

Oto jak wyglądałoby odliczanie przy użyciu pętli `for` lub innej metody, o której jeszcze nie wspominaliśmy, `rev`, w celu odwrócenia zakresu:

<span class="filename">Plik: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-34-for-range/src/main.rs}}
```

Ten kod jest trochę ładniejszy, prawda?

## Podsumwanie

Zrobiłeś to! To był spory rozdział: nauczyłeś się o zmiennych, skalarnych i złożonych typach danych, funkcjach, komentarzach, wyrażeniach `if` i pętlach! Jeśli chcesz przećwiczyć koncepcje omówione w tym rozdziale, spróbuj zbudować programy wykonujące następujące czynności:

* Konwersja temperatur między stopniami Fahrenheita i Celsjusza.
* Wygeneruj n-tą liczbę Fibonacciego.
* Wydrukuj tekst kolędy „The Twelve Days of Christmas”, korzystając z powtórzeń w piosence.

Kiedy będziesz gotowy, aby przejść dalej, porozmawiamy o koncepcji w Rust, która nie występuje powszechnie w innych językach programowania: ownership.

[comparing-the-guess-to-the-secret-number]:
ch02-00-guessing-game-tutorial.html#porwnywanie-odpowiedzi-gracza-z-sekretnym-numerem
[quitting-after-a-correct-guess]:
ch02-00-guessing-game-tutorial.md#wychodzenie-z-programu-po-poprawnym-odgadniciu-liczby
