---
description: Programsko inženjerstvo - Vue.js
author: Nikola Tanković
license: CC BY-SA
---

<img src="art/fipu.png" alt="fipu" style="zoom:24%;" />

# Vue.js - Spremanje dodatnih korisničkih podataka

U ovoj vježbi prikazivat ćemo mogućnost spremanja dodatnih korisničkih podataka uz registraciju.

## Koraci

1. Kod sa prethodnih VUE-05 vježbi možemo preuzti s GitHuba. Repozitorij: https://github.com/dbulic/instaclone (branch `plan-wk6`). Preuzimanje s Git-a, instaliranje paketa i pokretanje aplikaciije pojašnjeno je u prethodnim vježbama.

1. Prvo ćemo dodati prikazivanje greške prilikom registracije u `Signup.vue`. Koristit ćemo Bootstrap traku za prikaz grešaka:
  
  ```html
  <div class="alert alert-danger">
    <strong>Ups!</strong>
    Došlo je do greške.
  </div>
  ```
  
  Kako bi spriječili da se navedena greška stalno prikazuje, postavit ćemo novu varijablu u `data()` i pomoću `v-if` direktive kontrolirati prikaz i sadržaj greške:
  
  ```html
  ...
  	<div v-if="errorMessage" class="alert alert-danger">
      <strong>Ups!</strong>
      {{ errorMessage }}
    </div>
  ...
  
  <script>
  import store from "../store";
  export default {
    data() {
      return {
        errorMessage: "", // defaultno prazno, pa se greška ne prikazuje
  
        ...
  ```
  
1. Navedenu grešku postavit ćemo u `.catch()`dijelu Firebase metode za registraciju:

   ```javascript
   //...
   methods: {
       signup() {
         firebase
           .auth()
           .createUserWithEmailAndPassword(this.email, this.password)
           .then(() => {
             // ...
           })
           .catch(error => {
             console.error(error);
             this.errorMessage = error.message; // postavljanje poruke s greškom
           });
       }
     }
   };
   ```

   Na taj način prikazat će se pogreška prilikom registracije.

1. Sada ćemo dodati mogućnost da korisnik odabere vrstu profila. Pritom će nam poslužiti `<select>` element koji opcije povlači iz varijable `tipProfila`. Prvo ćemo dodati `tipProfila: ["Javni", "Privatni"],` u `data()` a zatim novi element u formu koji odabrani profil sprema u varijablu `odabraniTipProfila`(također ju treba dodati u `data()`):

   ```html
   <div class="form-group">
     <label for="tipProfila">Tip profila</label>
     <select v-model="odabraniTipProfila"
             id="tipProfila"
             class="form-control form-control-lg">
       <option v-for="k in tipProfila">{{k}}</option>
     </select>
   </div>
   ```

   Zatim ćemo modificirati metodu za registraciju korisnika koja će nakon uspješne registraciju u novu kolekciju `users`spremiti dodatne podatke o korisniku. Kao `id` zapisa možemo koristiti korisnički `email`jer je jedinstven:

   ```javascript
   methods: {
       signup() {
         firebase
           .auth()
           .createUserWithEmailAndPassword(this.email, this.password)
           .then(() => {
             // postavi podatke o korisniku
             let id = this.email;
             // sada moramo spremiti te dodatne podatke
             db.collection("users")
               .doc(id)
               .set({
                 tipProfila: this.odabraniTipProfila
               })
               .then(function() {
                 console.log("Document successfully written!");
               })
               .catch(function(error) {
                 console.error("Error writing document: ", error);
               });
           })
           .catch(error => {
             console.error(error);
             this.errorMessage = error.message;
           });
       }
     }
   ```

1. Ono što nam je još potrebno jest dohvatiti te dodatne podatke o korisniku nakon uspješne prijave. To možemo načiniti u komponenti `App.vue` nakon provjere da je korisnik autentificiran:

   ```javascript
   //...
   if (user) {
     self.userEmail = user.email;
     self.authenticated = true;
     
     // novi kod:
     db.collection("korisnici")
     .doc(user.email)
     .get()
     .then(doc => {
         if (doc.exists) {
           console.log("Document data:", doc.data());
           this.tipKorisnika = doc.data().tipProfila;
         } else {
           // doc.data() will be undefined in this case
           console.log("No such document!");
         }
   	});
     //...
   ```

   Dodatni podatak sprema se u `tipKorisnika`koji je potrebno inicijalizirati u `store.js`.

   

   

