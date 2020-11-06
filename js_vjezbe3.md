---
description: Programsko inženjerstvo - JS - Zadaci za vježbanje
author: Toni Starčić, Nikola Tanković
license: CC BY-SA
---

<img src="art/fipu.png" alt="fipu" style="zoom:24%;" />



1. Implementirajte funkciju koja prima polje binarnih znamenki s time da je broj indeksa polja fiksan:

  ```javascript
  INPUT => [0, 0, 0, 0, 0, 0, 1, 0]
  OUTPUT => f(INPUT) //2
  ```

2. Implementirajte funkciju koja prima *string*, a vraća broj koji nedostaje u tom *stringu*, tj. nizu brojeva:

  ```javascript
  INPUT => "1235678";
  OUTPUT => f(INPUT) //4;
  INPUT => "9091929495";
  OUTPUT => f(INPUT) //93;
  ```

3. Implementirajte rekurzivnu funkciju koja računa produkt ***Fibonaccijevih*** brojeva s time da ne uzima u obzir početnu iteraciju. Napišite ju na način da prima argument *n*:

  ```javascript
  INPUT => 6
  OUTPUT => f(INPUT) //30
  ```

  **DODATNO POJAŠNJENJE**: 0 - 1 - 1 - 2 - 3 - 5 (preskače 0).

4. Implementirajte rekurzivnu funkciju koristeći već ugrađene funkcije *map* i *filter*, koja prima prirodni broj *n* i vraća polje trojki čiji je opseg maksimalno *n*:

  ```javascript
  INPUT => 12
  OUTPUT => f(INPUT) //[3,4,5]
  ```

  **DODATNO POJAŠNJENJE**: Elementi liste su stranice trokuta "a", "b" i "c". Moraju biti pitagorine trojke i opseg tih stranica mora biti manji ili jednak n.

