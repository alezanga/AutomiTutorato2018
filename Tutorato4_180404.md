<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Grammatiche CFG](#grammatiche-cfg)
	- [Es dalle slide 1 CFG](#es-dalle-slide-1-cfg)
		- [Es 5.1.1.d](#es-511d)
			- [SE (<=) (Se una stringa è in L(S), allora contiene un numero di 0 doppio di quello degli 1)](#se-se-una-stringa-in-ls-allora-contiene-un-numero-di-0-doppio-di-quello-degli-1)
			- [Lemma  utile](#lemma-utile)
			- [SOLO SE (=>) (Se una stringa contiene un numero di 0 doppio di quello degli 1 allora è in L(S))](#solo-se-se-una-stringa-contiene-un-numero-di-0-doppio-di-quello-degli-1-allora-in-ls)
	- [Altri esercizi](#altri-esercizi)
		- [Esercizio T1 (da esame)](#esercizio-t1-da-esame)
			- [DIMOSTRAZIONE: A e B producono stringhe in (ripettivamente) K e J.](#dimostrazione-a-e-b-producono-stringhe-in-ripettivamente-k-e-j)
			- [DIMOSTRAZIONE: Qualunque stringa in K e J è prodotta da A e B](#dimostrazione-qualunque-stringa-in-k-e-j-prodotta-da-a-e-b)
			- [Dimostrazione di S.](#dimostrazione-di-s)
		- [Es 5.1.7.a libro](#es-517a-libro)

<!-- /TOC -->
# Grammatiche CFG
## Es dalle slide 1 CFG
### Es 5.1.1.d
Scrivere una CFG per L<sub>d</sub> = {insieme delle stringhe in {0,1}* con numero di 0 doppio del numero di 1}

**S** => S0S0S1S | S0S1S0S | S1S0S0S | &epsilon;

Ora va dimostrato che `w` &isin; L<sub>d</sub> se e solo se (<=>) `S` *=> `w`
DIMOSTRAZIONE:

#### SE (<=) (Se una stringa è in L(S), allora contiene un numero di 0 doppio di quello degli 1)
Si procede per induzione sul numero di passi di derivazione.

CASO BASE: n = 1

Allora w = &epsilon; che &isin; L<sub>d</sub>.

INDUZIONE: n &ge; 2

L'ipotesi induttiva è che l'enunciato sia corretto per `n` passi di derivazione. Pertanto si suppone che se `S` *=> `x` in `n` passi allora `x` ha \#0 doppio di \#1.

Siano *x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>, x<sub>4</sub>* stringhe prodotte da `S` in `n` passi di derivazione. Allora con un passo in più si possono produrre le stringhe:
1. S => S0S0S1S (n)=> x<sub>1</sub>0x<sub>2</sub>0x<sub>3</sub>1x<sub>4</sub>
2. S => S0S1S0S (n)=> x<sub>1</sub>0x<sub>2</sub>1x<sub>3</sub>0x<sub>4</sub>
3. S => S1S0S0S (n)=> x<sub>1</sub>1x<sub>2</sub>0x<sub>3</sub>0x<sub>4</sub>


Queste stringhe hanno tutte il corretto numero di 0 e 1, se è valida l'ipotesi induttiva.

Per dimosrare il SE, torna utile questo lemma.
#### Lemma  utile
Ogni stringa in L<sub>d</sub> (escluso &epsilon;) è formata da triple t<sub>1</sub>t<sub>2</sub>...t<sub>k</sub> e contiene almeno una sottostringa con due `0` e un `1`, ovvero una sottostringa fra:
- `001`
- `010`
- `100`.

DIMOSTRAZIONE del lemma:

Ovviamente per stringhe come `001 010` è banalmente vero visto che sono formate proprio da quelle stringhe. Ma ad esempio
`000 110` non è formata da tali stringhe, anche se è in L<sub>d</sub>.

Se una stringa non è costituita da nessuna tripla fra quelle elencate sopra, allora deve essere costituita di triple con due o tre `1`. Ma allora per essere in L<sub>d</sub> dovrà anche avere qualche tripla di soli `0`, per 'compensare' gli `1`. Ma concatenando triple con due o tre `1` con triple `000` sicuramente otterremo almeno una tripla con due `0` e un `1` (come ad esempio nella stringa `000 110` = 0 `001` 10). Per cui &forall; `w` &isin; L<sub>d</sub>, `w` sarà nella forma `x m y` dove `xy` &isin; L<sub>d</sub> e
`m` = 001/010/100.


#### SOLO SE (=>) (Se una stringa contiene un numero di 0 doppio di quello degli 1 allora è in L(S))

CASO BASE: |w| = 0 ==> w = &epsilon; che &isin; L(S).

INDUZIONE: |w| &ge; 1

Suppongo che esistano produzioni per generare tutte le stringhe in L<sub>d</sub> di lunghezza `3*n` (sono sempre multipli di 3 per il lemma sopra).
Dimostro che è possibile generare qualunque stringa `w` di lunghezza `3*(n+1)`. Allora per il lemma precedentemente dimostrato `w` = `x m y` e `xy` &isin; L<sub>d</sub> e `m` = 001/010/100. Allora uso l'ipotesi induttiva su `xy`. Per cui esiste una produzione `S *=> xy`. Più precisamente, per come sono fatte le produzioni, `S` genererà una cosa in questa forma: `S *=> x S y`, visto che fra ogni coppia di terminali c'è una variabile `S`.

A questo punto basta inserire la stringa `m` con una delle tre produzioni, togliendo le `S` in eccesso con la produzione
S => &epsilon;


### Esercizio 3 pag 25 slides
Scrivere una CFG per L.

L = {a<sup>n</sup>b<sup>m</sup> | 0 ≤ n ≤ m ≤ 2n}

Grammatica:
- **S** => aSBb | &epsilon;
- B => b | &epsilon;

Va dimostrato che `w` &isin; L <=> `w` è generata da S.

#### Dimostro =>
Per induzione su |w|= n.

CASO BASE:
- |w| = 0. Allora w = &epsilon; e c'è la produzione S => &epsilon;

INDUZIONE: (n &ge; 2)

Allora se ho una stringa `w` &isin; L e |w| &ge; 2, può essere scritta in (almeno) una delle due forme:

1. `w1 = a x b`, con `x` &isin; L.
2. `w2 = a y bb`, con `y` &isin; L.

Allora suppongo per ipotesi induttiva che sia `x` che `y` siano generate da S.

Quindi posso usare queste produzioni, nei rispettivi casi, per ottenere `w1` e `w2`:

1. S => aSBb => a x B b => `a x b` = w1.
2. S => aSBb => a y B b => `a y bb` = w2.

Per cui supponendo che tutte le stringhe in L, lunghe `n` siano generate, posso produrre tutte quelle lunghe `n+2` e `n+3`.

#### Dimostro <=
Per induzione su `n` = # di passi di derivazione.

CASO BASE:
- n = 1: S => &epsilon;, che è una striga del linguaggio.

INDUZIONE: n &ge; 2

S => aSBb (n-1)=> a x B b.

Uso l'ipotesi induttiva per sostenere che `x` &isin; L. Allora:

1. `axb`
2. `axbb`

sono entrambi in L.





## Altri esercizi
### Esercizio T1 (da esame)

**S** => aB

B => Ab | b

A => aB | a

Data la CFG, definire il suo linguaggio. E dimostrare induttivamente che S genera tale linguaggio.

A produce stringhe a<sup>n</sup>b<sup>m</sup> con n = m+1 oppure n = m, n > 0 e m &ge; 0. Chiamo il linguaggio K.
B produce stringhe a<sup>n</sup>b<sup>m</sup> con m = n+1 oppure n = m, m > 0 e n &ge; 0. Chiamo il linguaggio J.

S allora produce il linguaggio L = {w | w = a<sup>n</sup>b<sup>m</sup> con `n` = `m` oppure `n` = `m+1` con `n` e `m` > 0}.

Ora va dimostrato che `w` &isin; L(S) <=> `w` &isin; L.
Conviene però prima dimostrare induttivamente che le variabili A e B producono il liguaggi K e J, poi, sapendo questo, segue facilmente che S genera tutte e sole le stringhe in L.

#### DIMOSTRAZIONE: A e B producono stringhe in (ripettivamente) K e J.

Devo dimostrare che:
1. w è prodotta da A => w &isin; K.
2. w è prodotta da B => w &isin; J.


CASO BASE 1 passo:
A => a e B => b che sono stringhe in K e J.

INDUZIONE 2+ passi:
Assumiamo che valga l'ipotesi induttiva per stringhe prodotte in  `n` &ge; 1 passi.

A => aB (n)=> ax. Allora `x` &isin; J per ipotesi induttiva. Allora `ax` è generata in n+1 passi e sicuramente &isin; K perchè aggiungendo una 'a' davanti semplicemente o pareggio il numero di 'a' e 'b', oppure avrò una 'a' in più.

B => Ab (n)=> xa. Su `x` vale l'ipotesi induttiva perchè è prodotta da A in n passi.



#### DIMOSTRAZIONE: Qualunque stringa in K e J è prodotta da A e B

CASO BASE: |w| = 1.
`w = a` e `w = b` che sono generate.

INDUZIONE |w| &ge; 2:

Devo dimostrare che:

1. w1 &isin; K => w1 è prodotta da A.
2. w2 &isin; J => w2 è prodotta da B.

Sia `n` = |w1| = |w2|

Siano:

- w1 &isin; L(A)
- w2 &isin; L(B)

Allora:

- w1 = `a x1` con `x1` = a<sup>n</sup>b<sup>m</sup> con `m = n` oppure `m = n+1`, `m > 0` e `n` &ge; 0.
- w2 = `x2 b` con `x2` = a<sup>n</sup>b<sup>m</sup> con `n = m` oppure `n = m+1`, `n` > 0 e `m` &ge; 0.

Quindi `x1` &isin; `J` e `x2` &isin; `K`.

Suppongo per ipotesi induttiva che i punti `1` e `2` siano validi per stringhe lunghe `n-1`.

Allora `A *=> x2` e `B *=> x1`.

E quindi w1 e w2, che contengono almento due simboli sono prodotte da:

1. A => aB *=> `a x1` = `w1`
2. B => Ab *=> `x2 b` = `w2`

Quindi è possibile generare qualunuqe stringa in K e J.

#### Dimostrazione di S.
S produce tutte le stringhe di B con una `a` all'inizio. Segue che la definizione di L è corretta.


### Es 5.1.7.a libro

Considero la CFG: **S** => aS | Sb | a | b

Dimostrare per induzione sulla lunghezza delle stringhe che nessuna sringa `w` in L(S) ha `ba` come sottostringa.

CASO BASE: |w| = 1 e |w| = 2

- w = a
- w = b
- w = aa
- w = ab
- w = bb

Non si può generare `ba`.

INDUZIONE: |w| &ge; 2

Suppongo che tutte le stringhe lunghe `n` non contengano `ba`.
Allora:

1. S => aS *=> ax = `w`
2. S => Sb *=> xb = `w`

Allora se `x` non contiene `ba` in entrambi i casi anche `w` non conterrà `ba`.
