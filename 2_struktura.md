---
description: Programsko inženjerstvo - Struktura programa
author: Nikola Tanković
license: CC BY-SA
---

<img src="art/fipu.png" alt="fipu" style="zoom:24%;" />

# Programsko inženjerstvo - Vježbe

## 2. Struktura programa

_(prilagođeno prema knjizi Eloquent Javascript)_

Sav Javascript se može isprobati u konzoli internet preglednika ili na adresi https://jsconsole.com/.

U prethodnom smo poglavlju upoznali osnovne Javascript tipove vrijednosti, te unarne i binarne operatore nad njima. Potrebno je kombinirati vrijednosti i operatore u složenije izraze koje stvaraju nove vrijednosti. 

Vrijednosti se pohranjuju u varijablama koje predstavljaju **stanje** programa. Varijable je potrebno deklarirati (ključna riječ `let`), a zatim im i postaviti vrijednost pomoću operatora `=`.

```javascript
let varijabla; // deklaracija
varijabla = 10; // postavljanje vrijednosti

let nova_varijabla = 11; // ... u jednom koraku

console.log(varijabla, nova_varijable)
```

Postoji i posebna vrsta varijable `const` kojoj nije dozvoljeno promijeniti jednom inicijaliziranu vrijednost.

```javascript
const konstanta = 3.14;
konstanta = konstanta + 1; //TypeError!
```

Varijable u Javascriptu mogu početi bilo kojim slovom te znakovima `$` i `_`.

**Okruženje.** Skup svih pridruženih vrijednosti varijabli naziva se okruženje. Pri pokretanju programa već postoji set unaprijed definiranih varijabli, primjerice varijabla `console`. Takve predefinirane varijable omogućuju komunikaciju s ostalim djelovima sustava (npr. ispis, čitanje korisničkih podataka, ...).

**Funkcije.** Tip "funkcija" u Javascriptu predstavlja dio programa koji je potrebno izvršiti vezan uz neki naziv (_binding_). Za razliku od ostalih programskih jezika, funkcije su vezane uz naziv kao i varijable, s tom razlikom da ih je moguće izvršiti (pozvati). Pozivanje se izvršava tako da se nakon naziva varijable koja sadrži funkciju napišu zagrade s listom argumenata `(`i `)`.

```javascript
// prompt je funkcija za unos podataka
prompt(); // poziv bez argumenata
prompt("Unesi neki broj"); // poziv s argumentima
```

Kako su funkcije vezane uz naziv kao i varijable, moguće ih je čak promijeniti da označavaju nešto drugo.

Primjer:

```javascript
var a = prompt("Unesi neki broj:");
console.log(a);
prompt = "više nisam funkcija";
var b = prompt("Unesi neki broj:") // TypeError!
```

**Uvjetno izvođenje**. Uvjetno izvođenje određeno je ključnom riječi `if` i `else` te se ponaša slično kao u programskom jeziku C.

```javascript
let theNumber = Number(prompt("Odaberi jedan broj"));
if (!Number.isNaN(theNumber)) {
  console.log("Odabrao si korijen od broja " +
              theNumber * theNumber);
}
```

_Pitanje: čemu služi funkcija **Number ** iz primjera?_

**Petlje.** Postoje tri vrste petlji u Javascriptu:

1. `while ` petlja
1. `do while` petlja
1. `for` petlja

Primjeri:

```javascript
let result = 1;
let counter = 0;
while (counter < 10) {
  result = result * 2;
  counter = counter + 1;
}
console.log(result);
// → 1024
```

```javascript
let yourName;
do {
  yourName = prompt("Who are you?");
} while (!yourName);
console.log(yourName);
```

```javascript
for (let number = 0; number <= 12; number = number + 2) {
  console.log(number);
}
```

Slično kao i u C-u, ukoliko je potrebno prekinuti izvođenje petlje, možemo to učiniti pomoću ključne riječi `break`, dok sa `continue` preskačemo ostatak trenutnog izvođenja i prelazimo na sljedeće ponavljanje.

## Zadaci za vježbu

1. **(JS-201)** Napiši petlju koja će ispisati u konzolu sljedeće

   ```
   #
   ##
   ###
   ####
   #####
   ```

1. **(JS-202)** FizzBuzz. Napiši program koji će ispisati sve brojeve od 1 do 100 uz dvije iznimke. Ukoliko je broj djeljiv s 3 umjesto njega će ispisati "Fizz", ukoliko je djeljiv s 5, umjesto njega će ispisati "Buzz", a ako je djeljiv s 3 i 5, ispisat će umjesto njega "FizzBuzz".

1. **(JS-203)** Napiši program koji ispisuje šahovsko polje koristeći razmak (`" "`) i znak `#`:

   ```javascript
    # # # #
   # # # # 
    # # # #
   # # # # 
    # # # #
   # # # # 
    # # # #
   # # # #
   ```

   Napravi program tako da postoji na početku definirana varijabla `velicina` koja označava veličinu kvadrata (npr `let velicina = 5`.