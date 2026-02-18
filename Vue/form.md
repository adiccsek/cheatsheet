## 📌 Form események Vue-ban

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