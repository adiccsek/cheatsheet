1. Mi az a HTML forma?

A form egy HTML elem, ami lehetővé teszi az adatbevitel felhasználók számára.

Példák: szöveges mező, jelszó, rádiógomb, jelölőnégyzet, legördülő lista, gomb.

Formák tipikusan adatokat küldenek a szervernek vagy a frontendnek feldolgozásra.

Alap szintaxis:
```html
<form action="/submit" method="POST">
  <input type="text" name="username" placeholder="Felhasználó név">
  <input type="password" name="password" placeholder="Jelszó">
  <button type="submit">Küldés</button>
</form>
```

```
action → hova küldjük az adatot
method → milyen HTTP módszerrel (GET, POST)
```

## 📌 2. Fontos HTML input típusok
```
Típus	Mire való?
text	Egyszerű szöveg
password	Jelszómező (karaktereket elrejti)
email	Email cím ellenőrzéssel
number	Csak számot fogad
checkbox	Többválasztós jelölőnégyzet
radio	Egymást kizáró választás
textarea	Többsoros szöveg
select	Legördülő lista
```

## 📌 3. Formázás és azonosítás

```
name → a szerver a name attribútum alapján azonosítja az adatot

id → egyedi azonosító, labelhez kapcsolható

placeholder → helykitöltő szöveg, ami segíti a felhasználót
```
```html
<label for="email">Email:</label>
<input type="email" id="email" name="email" placeholder="pl. valaki@example.com">
```

## 📌 4. Submit gomb
```html
<button type="submit">Küldés</button>
```

A form elküldéséhez szükséges.
Ha nincs type, a button alapból submit.

## 📌 5. Form események Vue-ban

A v-model köti az inputot a Vue komponens adatához (reactive state).

A submit esemény feldolgozható JavaScript-tel, hogy ne töltse újra az oldalt:
```html
<form @submit.prevent="handleSubmit">
  <input v-model="username" placeholder="Felhasználó név">
  <button type="submit">Küldés</button>
</form>

<script>
<template>
  <!-- @submit.prevent → figyeli a submit eseményt és megakadályozza az alap HTML újratöltést -->
  <form @submit.prevent="handleSubmit">

    <!-- v-model="username" → kétirányú kötés: ami a felhasználó gépel, az a data.username-be kerül -->
    <input v-model="username" placeholder="Felhasználó név">

    <!-- 🔹 Submit gomb -->
    <!-- type="submit" → ha rákattintanak, elindítja a form submit eseményt -->
    <button type="submit">Küldés</button>
  </form>
</template>

<script>
export default {
  // 🔹 Komponens adatainak deklarálása
  data() {
    return {
      // username → ide kerül a felhasználó által beírt szöveg
      username: ""
    };
  },

  // 🔹 Komponens metódusai
  methods: {
    // 🔹 Form submit esemény kezelése
    handleSubmit() {
      // console.log → itt látjuk a felhasználó által beírt értéket
      console.log("Beírt név:", this.username);

      // Itt tudnánk pl. POST-olni az adatot egy API-ra Axios-szal
      // axios.post('/api/submit', { name: this.username })
    }
  }
};
</script>
```

```
@submit.prevent  → megakadályozza az oldal újratöltését (alap HTML viselkedés)
```