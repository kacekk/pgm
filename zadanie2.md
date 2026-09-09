# Zadanie 2

> Dostajesz pytanie, czy zawodnik X nadaje się na wahadłowego w naszym systemie. Masz dane StatsBomb z jego 20 meczów. Opisz, jak byś do tego podszedł i gdzie te dane Cię zawiodą.

---

## Odpowiedź

### Zanim otworzę dane, pytam trenera, o jakiego wahadłowego chodzi.

Wahadłowy jest bardzo różnorodną rolą, która może mieć różne twarze. Może dobiegać do linii końcowej i dośrodkowywać, lub schodzić do środka i szukać podania/strzału, to dwa różne typy zawodników. Do tego dochodzi, czy dochodzi do tranzycji między fazami ofensywnymi i defensywnymi czyli np. z 3 obrońców na 4 lub czy np. przy stracie wraca do piątki, czy zostaje wysoko i z której gra strony.

### Potem sprawdzam, czy w tych 20 meczach jest to, czego szuka klub.

20 meczów to nie znaczy 20 meczów na wahadle. Sprawdzam, na jakiej pozycji faktycznie grał -> StatsBomb podaje to przy każdym evencie i w ustawieniach z `Starting XI` oraz `Tactical Shift`. Jeśli w połowie z nich był bocznym obrońcą w czwórce, to jego liczby mówią o innym założeniu niż to, którego szuka klub.

Patrzę też, ile realnie zagrał minut, po której stronie, z kim grał i jak wyglądał wynik. To ostatnie ma znaczenie, bo wahadłowy przy prowadzeniu i przy przegrywaniu robi zupełnie co innego, dokładnie ten sam podział co w zadaniu 1, tylko tutaj przydaje się praktycznie. Warto również zapytać, kto te dane przygotował, jeżeli agent zawodnika to wiadomo że będzie chciał jak najlepiej go przedstawić. Jeżeli bierzemy po prostu ostatnie 20 meczów, problem w pewnym sensie znika i mniej więcej znamy jego aktualną formę.

### Dopiero teraz zaczyna się praca na liczbach.

Do każdego wymagania z listy trenera dobieram jedną–dwie rzeczy, które da się policzyć:

| Czego trener chce | Na co patrzę |
|---|---|
| Trzyma szerokość i wysokość | gdzie ma kontakty z piłką, ile z nich w ostatniej tercji |
| Dowozi piłkę do przodu | prowadzenia wchodzące w ostatnią tercję i w pole karne, wartość jego prowadzeń i podań (OBV) |
| Kreuje z boku | dośrodkowania i podania odwrotne, ile z nich dochodzi, asysty i podania przy strzale |
| Wygrywa 1v1 w ataku | dryblingi: ile prób, ile udanych |
| Broni 1v1 | ile razy go minięto, pojedynki obronne, przechwyty, gdzie na boisku to robi |
| Pracuje w pressingu | pressing, kontrpressing, odbiory na połowie rywala |
| Ogarnia pod presją | jak podaje, kiedy jest kryty — czy gra trudne piłki, czy tylko bezpieczne |

Dwie ważne rzeczy, których nie można pominąć. Po pierwsze, porównuję go do innych wahadłowych z tej ligi, a nie patrzę na gołe liczby, „3 dośrodkowania na mecz" nic nie znaczy, dopóki nie wiem, ile robią inni. Po drugie, patrzę na rozrzut mecz po meczu, nie na średnią. Zawodnik z czterema dośrodkowaniami w każdym meczu i taki z dwudziestoma w jednym i zerem w reszcie mają tę samą średnią i zupełnie inną wartość.

Na koniec zestawiam to z wahadłowymi, których klub ma teraz. Pytanie nie brzmi „czy jest dobry", tylko „czy jest lepszy od tego, co klub już ma, w tych kilku rzeczach, na których mu zależy" lub "czy jest godnym rezerwowym/młodym zawodnikiem z potencjałem itp"

### Końcowa wideoweryfikacja.

Z danych wyciągam sytuacje do obejrzenia: wszystkie obrony 1v1 w swojej tercji, wszystkie dojścia do linii końcowej, zachowanie po stracie. Trener ogląda i ocenia to, czego w liczbach nie widać. Cała robota z danymi ma skrócić oglądanie z 20 meczów do kilkudziesięciu klipów, a nie je zastąpić.

---
## Gdzie te dane mnie zawiodą?

**Wahadłowy pracuje bez piłki, a te dane widzą tylko piłkę.** To jest największy problem i nie da się go obejść. Zawodnik dotyka piłki może 70 razy w meczu, czyli jakieś półtorej minuty. Cała reszta — czy stoi tam, gdzie powinien, kiedy rusza w wolne miejsce, czy wraca na czas do piątki, czy trzyma linię z resztą obrony — po prostu w tych danych nie istnieje. A to jest większość jego roboty. Freeze frame'y, czyli ustawienie zawodników, są tylko przy strzałach, więc nawet tego nie ma jak prześledzić na podstawie samych danych.

**Nie wiem nic o jego bieganiu.** Wahadłowy biega najwięcej z całej drużyny — sprint w przód, powrót 60 metrów, i tak przez cały mecz. Bez trackingu nie jestem w stanie odpowiedzieć, ile z tego zostaje w nim w 85. minucie. Jeśli klub ma dostęp do danych trackingowych albo StatsBomb 360, spora część tych zastrzeżeń znika.

**Jego liczby to jego drużyna, nie ta, do której miałby trafić.** Jeśli grał w czwórce, która rzadko przechodziła w trójkę, to miał krótszy odcinek do pokrycia i inne zadania przy stracie niż w systemie, do którego miałby wejść, gdzie ma domykać piątkę. Niska liczba dośrodkowań mówi wtedy o systemie jego drużyny, a nie o tym, czy on to potrafi. Tego żadna metryka nie naprawi. Mogę tylko uczciwie powiedzieć, na ile jego dotychczasowa gra przypomina tą, której oczekuje klub.

**20 meczów starcza na jedne rzeczy, na inne nie.** Podań i kontaktów z piłką ma po kilkadziesiąt na mecz, więc te liczby są wiarygodne. Ale dośrodkowań w pole karne czy obron 1v1 jest po kilka, przy 20 meczach różnica między nim a zawodnikiem, którego klub ma teraz, najczęściej mieści się w granicy błędu. Nie można pozwolić aby niewielka różnica zagrała dużą rolę, w kwestii finalnego transferu lub rezygnacji.

**Poziom ligi.** Te same akcje w słabszej lidze są po prostu łatwiejsze przez niższy poziom przeciwników. Porównanie do innych z jego ligi trochę to wyrównuje, ale przeskok między ligami zawsze zostaje czymś czego nie możemy być do końca pewni, tak samo jak adaptacji w nowej drużynie.

**Model nie płaci za dobre ustawienie.** Modele wyceniają to, co zawodnik zrobił z piłką. Wahadłowy, który przez cały mecz trzyma szerokość i wyciąga rywala, robiąc miejsce koledze, nie zostaje przez to odpowiednio nagrodzony przez model.

**Reszta jest poza danymi.** Kontuzje i to, ile już wybiegał, wiek, charakter, dogadywanie się z trójką stoperów, adaptacja do nowej ligi, to aspekty, których bezpośrednio z pliku nie dostaniemy i potrzebna jest indywidualna obserwacja zawodnika.

---

## Co bym oddał trenerowi

Jedną stronę: te 5–6 rzeczy, o które pytał, przy każdej gdzie zawodnik jest na tle ligi i na tle zawodników klubu, wyraźnie zaznaczone, których dwóch–trzech rzeczy dane nie rozstrzygają, i kilkadziesiąt klipów do obejrzenia. Do tego zdanie, czego bym potrzebował, żeby domknąć temat — zwykle danych o bieganiu i obejrzenia go pod kątem samego ustawiania się bez piłki.
