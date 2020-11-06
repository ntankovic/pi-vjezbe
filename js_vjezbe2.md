---
description: Programsko inženjerstvo - JS - Zadaci za vježbanje
author: Toni Starčić, Nikola Tanković
license: CC BY-SA
---

<img src="art/fipu.png" alt="fipu" style="zoom:24%;" />



1. Implementirajte funkciju koja prima polje *stringova* i vraća najkraći *string*: 

```javascript
INPUT => ["aaa", "bbbb", "cc", ""]
OUTPUT = f(INPUT) //"cc"
```

2. Implementirajte funkciju koja računa ***manhattanDistance*** s time da su točke x1, y1, x2 i y2 članovi *polja*:

```javascript
INPUT => ([5,4],[3,2])
OUTPUT = f(INPUT) //4
```

3. Implementirajte funkciju koja prima *polje* i vraća *polje* u kojemu se nalaze podaci koji se pojavljuju točno jednom:

```javascript
INPUT => [1, 2, 1, 3, 1, 4, 1, 5, "a", "a", "b", "c"]
OUTPUT = f(INPUT) //[1, 2, 3, 4, 5, "a", "b", "c"] 
```

4. Implementirajte rekurzivnu funkciju koja prima *polje* podataka i prirodni broj *n*, a vraća *polje* elemenata koji se pojavljuju barem *n* puta.

```javascript
INPUT => ([1, 2, 1, 3, "a", 1, 4, 1, 5, "a", "a", "b", "c"], 2)
OUTPUT = f(INPUT) //[1, a]
```

**DODATNO POJAŠNJENJE**: U primjeru, 1 i "a" se pojavljuju 3 puta te iz tog razloga čine elemente *polja* outputa.