---
description: Programsko inženjerstvo - Vue.js
author: Nikola Tanković
license: CC BY-SA
---

<img src="art/fipu.png" alt="fipu" style="zoom:24%;" />

# Vue.js - Autentifikacija

U ovoj vježbi prikazivat ćemo jedan od načina na koji se može ostvariti autentifikacija u aplikaciji. Pritom ćemo koristiti Firebase bazu i JS pakete.

## Koraci

1. Kod sa prethodnih VUE-03 vježbi možemo pruezeti s GitHuba. Repozitorij: https://github.com/fipu-nastava/fipugram (branch `step3`). Preuzimanje s Git-a, instaliranje paketa i pokretanje aplikaicije pojašnjeno je u prethodnim vježbama.

1. Za korištenje Firebase-a u JavaScript/Vue aplikacije potrebno je uključiti Firebase module. Tu nam pomaže `npm` - upravitelj paketima.
  
```bash
   # u direktoriju projekta
   
   npm install --save firebase
```

3. U projektu ćemo napraviti novi JS modul `firebase.js` sa sljedećim sadržajem:

   ```javascript
   import firebase from 'firebase/app';
   import 'firebase/auth';
   import 'firebase/firestore';
   
   // zamiijeniti s vašom konfiguracijom!
   var firebaseConfig = {
       apiKey: 'ZAMIJENI ME!!',
       authDomain: 'fipugram.firebaseapp.com',
       projectId: 'fipugram',
       storageBucket: 'fipugram.appspot.com',
       messagingSenderId: 'ZAMIJENI ME!!!',
       appId: 'ZAMIJENI ME!!!',
   };
   // Initialize Firebase
   firebase.initializeApp(firebaseConfig);
   ```

   Time smo uključili potrebne `firebase`JavaScripte objekte u svoju aplikaciju. U ovom koraku otvorit ćemo novi Firebase račun (ukoliko ga već nemamo). Potrebno je izvršiti registraciju na https://firebase.google.com i ulogirati se na administracijsku konzolu: https://console.firebase.google.com/u/0/ i stvoriti novi Firebase projekt (nije nužno uključiti Firebase analytics).

4. Otvori svoj Firebase projekt i sa izbornika odaberi **Authentication**. Zatim odaberi **Set up sign-in method** i uključi (**Enable**) Email/Password način logina (za svoj projekt možeš podesiti i različite oblike logina poput Google ili Facebook logina).

   <img src="art/image-20191207154022809.png" alt="image-20191207154022809" style="zoom:50%;" />
   **Slika 1.**Izbornik Firebase konzole.

5. Još je potrebno u Vue projektu postaviti da se spaja na naš Firebase projekt. Do sada smo samo uključili Firebase biblioteke i omogućili autentifikaciju preko emaila i šifre. Podatke za spajanje na Firebase projekt možemo naći u Firebase konzoli u postavkama projekta (klik na zupčanik na izborniku) u sekciji **Firebabse SDK snippet** i podsekciji **CDN** (ili **Config**).
   <img src="art/image-20191207160309312.png" alt="image-20191207160309312" style="zoom:50%;" />
   **Slika 2.** Primjer Firebase konfiguracije.

   Navedenu konfiguraciju kopiramo i smjestimo u naš `firebase.js` modul.

6. Time je naša aplikacija povezana sa Firebaseom i možemo napraviti mogućnost registracije pomoću komponente `Signup.vue`. Prvo ćemo definirati Vue varijable za Email i dvije lozinke u `Signup.vue`:

   ```html
   <script>
   export default {
     data() {
       return {
         email: "",
         password: "",
         passwordRepeat: ""
       }
     }
   }
   </script>
   ```

   Zatim ćemo povezati navedene varijable sa `v-model`na odgovarajuća `input`polja u `<template>` sekciji:

   ```html
   <form>
           <div class="form-group">
             <label for="emailField">Email address</label>
             <input v-model="email" type="email" class="form-control" id="emailField" aria-describedby="emailHelp" placeholder="Enter email">
             <small id="emailHelp" class="form-text text-muted">We'll never share ...</small>
           </div>
           <div class="form-group">
             <label for="passwordField">Password</label>
             <input v-model="password" type="password" class="form-control" id="passwordField" placeholder="Password">
           </div>
           <div class="form-group">
             <label for="confirmPasswordField">Confirm Password</label>
             <input v-model="passwordRepeat" type="password" class="form-control" id="confirmPasswordField" placeholder="Confirm password">
           </div>
           <button type="submit" class="btn btn-primary mt-5">Sign up</button>
         </form>
   ```

   Potrebna nam je i nova metoda koja će učitati utipkane podatke i pozvati Firebase metodu za registraciju. Dodat ćemo je u `methods` sekciju:

   ```javascript
   export default {
     name: "signup",
     data() {
       return {
         email: "",
         password: "",
         passwordAgain: ""
       }
     },
     methods: {
       signup() {
         firebase.auth().createUserWithEmailAndPassword(this.email, this.password).catch(function(error) {
           console.log(error);
         });
       }
     }
   }
   ```

   Namjestit ćemo da se navedena metoda poziva prilikom *submita forme* (`<template>` dio u `Signup.vue`):

   ```html
   ...
   <form @submit.prevent="signup">
     ...
   ```

   Ukoliko je sve u redu trebali bi se moći registrirati i vidjeti novoga korisnika u Firebase konzoli (sekcija Authentication):

   ![image-20191207160416158](art/image-20191207160416158.png)

   

7. Na sličan način podesiti `Login.vue` komponentu. Potrebno je umjesto Firebase metode za *sign-up* koristiti metodu za *sign-in*. Možeš ju pronaći u Firebase dokumentaciji :)
   P.S. Razmisli jesu li potrebni baš identične varijable u `data` sekciji.

8. Registracija i Login sada rade. Međutim aplikacija je isto nezavisno o tome jeli trenutni korisnik ulogiran ili ne. U ovom ćemo koraku:

   * razlikovati kada je korisnik ulogiran i prema tome prikazati ili sakriti određene dijelove (npr. Login button),
   * nakon *logina* ili *logouta*preusmjeriti korisnika na `/home` ili `/login`.

   Da bi pratili stanje autentifikacije korisnika moramo dodati tzv. *listener*koji reagira na promjenu stanja autentifikacije (https://firebase.google.com/docs/reference/js/firebase.auth.Auth.html).

   U glavnu komponentu `App.vue` dodajemo sljedeći isječak:

   ``` javascript
   firebase.auth().onAuthStateChanged((user) => {
       if (user) {
           // User is signed in.
           console.log('*** User', user.email);
           store.currentUser = user.email;
       } else {
           // User is not signed in.
           console.log('*** No user');
           store.currentUser = null;
   
           if (router.name !== 'login') {
               router.push({ name: 'login' });
           }
       }
   });
   
   ```

   > :warning: **Razmisli**: zašto smo praćenje autentifikacije dodali u `App.vue`, a ne recimo u `Login.vue`?

   U `store.js` dodajemo varijablu `currentUser`pomoću koje ćemo razlikovati postoji li trenutni korisnik. Inicijalizirat ćemo varijablu na `null` čime naznačujemo da u početku ne postoji ulogirani korisnik.

   ```javascript
   // src/store.js
   
   export default {
       searchTerm: '',
       currentUser: null, // nova varijabla
   };
   ```

   Iskoristit ćemo `currentUser` varijablu za prikaz/sakrivanje login/logout buttona. Još je potrebno napraviti i *logout* akciju. Već imamo `logout` metodu u koju treba pozvati `Firebase` metodu za logout. Pronađi ju u dokumentaciji i zamijeni kod u postojećoj metodi. Zašto nije potrebno postaviti `store.currentUser = null`?

   ```html
   <!-- App.vue -->
   
   <ul class="navbar-nav ml-auto">
     <li v-if="!store.currentUser" class="nav-item">
       <router-link to="/login" class="nav-link">Login</router-link>
     </li>
     <li v-if="!store.currentUser" class="nav-item">
       <router-link to="/signup" class="nav-link">Sign up</router-link>
     </li>
     <li v-if="store.currentUser" class="nav-item">
       <a href="#" @click.prevent="logout()" class="nav-link">Logout</a>
     </li>
   </ul>
   ```

   

9. U zadnjem koraku još ćemo malo podesiti redirekciju i neovlašteni pristup nekim stranicama. Jedan od boljih načina na koji to možemo riješiti jest da uz svaku rutu u ruteru posebno naznačimo jeli potreban login za tu rutu. U tu svrhu ćemo koristiti `meta` podatke svake rute:

   ```javascript
   
   const routes = [
       {
           path: '/',
           name: 'home',
           component: Home,
           meta: { // dodajemo meta-podatke na home rutu jer je potreban login za nju
               needsUser: true, // možemo nazvati ovaj atribut kako želimo
           },
       },
       // ...
   ];
   ```

   Zatim radimo prilagodbu u `App.vue`:

   ```javascript
   firebase.auth().onAuthStateChanged((user) => {
       const currentRoute = router.currentRoute;
   
       if (user) {
           // User is signed in.
           console.log('*** User', user.email);
           store.currentUser = user.email;
   
           // take me home
           if (!currentRoute.meta.needsUser) {
               router.push({ name: 'home' });
           }
       } else {
           // User is not signed in.
           console.log('*** No user');
           store.currentUser = null;
   
           // kick me out
           if (currentRoute.meta.needsAuth) {
               router.push({ name: 'login' });
           }
       }
   });
   ```

   I kao dodatni vid sigurnosti dodat ćemo provjeru u trentku kada Vue mijenja rute, to možemo učiniti sa `beforeEach` metodom u ruteru:

   ```javascript
   import store from '@/store';
   
   // ...
   
   // dodajemo na dnu
   router.beforeEach((to, from, next) => {
       console.log('Bio sam na', from.name, 'idem na', to.name, 'a korisnik je', store.currentUser);
   
       const noUser = store.currentUser === null;
   
       if (noUser && to.meta.needsUser) {
           next('login');
       } else {
           next();
       }
   });
   
   export default router;
   ```

10. **Samostalni zadatak.** Provjeriti jesu li dvije lozinke iste pri registraciji. Napraviti novu stranicu postavki korisnika. Na toj stranici omogućiti korisniku promjenu lozinke. Zadatak predati na predviđeno mjesto pod šifrom VUE-04. 

