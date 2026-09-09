# xG przy różnych wynikach: Pogoń Grodzisk Mazowiecki

Polonia Bytom (PB) – Pogoń Grodzisk Mazowiecki (PGM) 2:2, dane StatsBomb, `match_id` 4068759.

Liczony z perspektywy Pogoni: ile xG stworzyli i ile stracili, osobno dla każdego wyniku na tablicy: gdy prowadzą, gdy jest remis i gdy przegrywają.

Kod: [`xg_by_game_state.ipynb`](xg_by_game_state.ipynb).

Nazwy kolumn: `xG_PGM` to Pogoń, `xG_PB` to Polonii z tego samego czasu, `xGD` to różnica. Stany: `leading` (prowadzenie) / `draw` (remis) / `trailing` (przegrywanie).

---

## Wynik

| state | minutes | shots_PGM | xG_PGM | xG_per_shot_PGM | shots_PB | xG_PB | **xGD** | xGD_per90 |
|---|---|---|---|---|---|---|---|---|
| leading | 6,5 | 2 | 0,117 | 0,059 | 2 | 0,079 | **+0,038** | +0,53 |
| draw | 78,5 | 10 | 0,609 | 0,061 | 17 | 0,923 | **−0,314** | −0,36 |
| trailing | 9,4 | 2 | 0,017 | 0,008 | 1 | 0,066 | **−0,050** | −0,48 |

Cały mecz: my 14 strzałów i 0,743 xG, oni 20 strzałów i 1,069 xG.

Ten sam podział przy konkretnych wynikach na tablicy (PGM:PB):

| score_PGM_PB | state_PGM | minutes | shots_PGM | xG_PGM | shots_PB | xG_PB | **xGD** |
|---|---|---|---|---|---|---|---|
| 0:0 | draw | 21,2 | 1 | 0,198 | 4 | 0,229 | **−0,032** |
| 1:0 | leading | 6,5 | 2 | 0,117 | 2 | 0,079 | **+0,038** |
| 1:1 | draw | 8,6 | 2 | 0,046 | 3 | 0,191 | **−0,145** |
| 1:2 | trailing | 9,4 | 2 | 0,017 | 1 | 0,066 | **−0,050** |
| 2:2 | draw | 48,7 | 7 | 0,365 | 10 | 0,503 | **−0,137** |

Trzy wiersze z `draw` sumują się na wiersz `draw` z tabeli wyżej.

## Co z tego widać

Prawie cały mecz to gra przy remisie, 78,5 z 94,4 minut. Prowadziliśmy tylko 6,5 minuty (między golem Losa a wyrównaniem), przegrywaliśmy 9,4 minuty. Nasz gol na 2:2 padł 37 sekund po przerwie, więc druga połowa w całości poszła przy remisie.

Przy remisie byliśmy gorsi: 10 strzałów i 0,609 xG do 17 strzałów i 0,923 xG, czyli **−0,314**. Nie było to jednak bicie: u obu drużyn wychodziło ok. 0,06 xG na strzał, czyli same przymiarki z dalszej odległości. W całym meczu nie padła ani jedna klarowna sytuacja, najlepsza miała 0,209 xG (Ciepiela, obroniona).

Liczby przy prowadzeniu i przy przegrywaniu to po 6–9 minut i po 1–2 strzały na stronę. Na tym nie da się powiedzieć nic o tym, jak drużyna gra przy prowadzeniu, dlatego kolumnę `xGD_per90` w tych dwóch wierszach lepiej zignorować. Żeby takie porównanie miało sens, trzeba zebrać kilkadziesiąt meczów.

## Jak to jest liczone?

- Stan meczu strzału = wynik tuż przed tym strzałem. Gol liczy się do stanu, w którym padł, i zmienia stan dopiero dla kolejnych zdarzeń.
- `xGD` = nasze xG minus xG rywala z tego samego kawałka meczu (nasze `leading` = ich `trailing`).
- Minuty w każdym stanie liczone z osi goli i długości połów, bez tego 6 minut i 78 minut nie da się porównać.
- Zegar sklejony przez połowy: StatsBomb w drugiej liczy od 45:00, więc surowy czas cofa się na przerwie. Granice z `Half End`: 45:05 + 49:19 = 94,4 min.
- W tym meczu nie było karnych ani czerwonych kartek, więc nic nie zaburza porównania.

**Uwaga do pliku:** ma 3892 wiersze przy 3232 eventach, bo każdy strzał jest powielony raz na zawodnika z freeze frame'u. Bez `drop_duplicates("id")` wychodzi 628 strzałów i 79 goli zamiast 34 i 4.

## Cztery gole

| czas | zespół | strzelec | xG | akcja | jak | dystans | rywale w linii | podanie |
|---|---|---|---|---|---|---|---|---|
| 21:13 | PGM | Kacper Los | 0,198 | rożny | głowa | 6 m | 3 | Ciepiela |
| 27:43 | PB | Lucjan Zieliński | 0,035 | po wrzucie | prawa noga | 19 m | 3 | brak (dobitka) |
| 36:18 | PB | Maciej Wolski | 0,093 | po wrzucie | głowa | 8 m | 2 | Zieliński |
| 45:37 | PGM | Radosław Majewski | 0,010 | po wznowieniu | lewa noga | 21 m | 2 | brak (przechwyt) |

Krótko, co się działo:

- **1:0 dla nas.** Rożny Ciepieli z lewej, główka Losa z 6 metrów. Najlepsza sytuacja, jaką stworzyliśmy w meczu.
- **1:1.** Nasza obrona wybiła piłkę po strzale Koniecznego, ale prosto pod nogi Zielińskiego, dobitka z 19 metrów. Sekunda między wybiciem a strzałem.
- **1:2.** Wrzut, Zieliński dochodzi do linii końcowej po prawej i dośrodkowuje, Wolski wchodzi w pole karne z drugiej strony i strzela głową z 8 metrów. Jedyny gol z regularnej akcji w polu karnym w całym meczu.
- **2:2.** 37 sekund po przerwie. Majewski przejmuje odbitą piłkę i strzela z 21 metrów z ostrego kąta z prawej. xG 0,010, czyli raz na sto takich prób.

Każda bramka ma w notebooku swoją mapkę z ustawieniem zawodników, torem strzału i podaniem, po którym padła.

## Mapka strzału

`plot_shot(shot_id)` rysuje pojedynczy strzał: kto gdzie stał (freeze frame), tor strzału i to, ile bramki było odsłonięte (żółte pole; białe wcięcia to rywale zasłaniający światło bramki). W nagłówku xG, efekt, rodzaj akcji, dystans i liczba rywali w linii strzału.

Sekcja 6 rysuje tak wszystkie cztery gole. Lista pozostałych strzałów z `id` jest w ostatniej komórce, wystarczy podać `id` do `plot_shot()`.

## Jak uruchomić

```bash
pip install pandas numpy matplotlib
jupyter lab xg_by_game_state.ipynb
```

CSV musi leżeć obok notebooka. Drużynę, z której perspektywy liczymy, zmienia się stałymi `PGM` / `PB` w drugiej komórce.

## Zadanie 2

Drugie zadanie, o ocenie zawodnika na wahadłowego z danych StatsBomb, jest w pliku [`zadanie2.md`](zadanie2.md).
