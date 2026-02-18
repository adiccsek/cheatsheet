# Általános
- 👉 HTTP kérést küld az endpoint felé
- 👉 megkapja a backend JSON válaszát
- 👉 JavaScript objektummá alakítja
- 👉 te pedig eltárolod és megjeleníted

A backend JSON-t ad vissza egy API endpointon,
és az Axios segítségével a frontend:
-   lekéri,
-   feldolgozza,
-   és megjeleníti azt.


## NPM használatával
``` npm install axios ```

## Yarn használatával
``` yarn add axios ```

Sikeres telepítés után az Axios importálható a Vue komponensekbe.

# Alap használat Vue-ban

Az Axios használatához importálni kell a komponensbe:

```js
 import axios from "axios"; 
 ```

Ezután az axios objektum metódusai segítségével indíthatók HTTP kérések.

## GET kérés

A GET kérés adatok lekérésére szolgál egy API végpontról.

Options API példa
```js
export default {
  // A komponens reaktív adatai
  data() {
    return {
      // Ebben a tömbben fogjuk tárolni a szervertől kapott felhasználókat
      users: []
    };
  },

  // A mounted lifecycle hook akkor fut le,
  // amikor a komponens már megjelent a DOM-ban
  mounted() {

    // HTTP GET kérés indítása az adott API végpontra
    axios.get("https://jsonplaceholder.typicode.com/users")

      // Ha a kérés sikeres (HTTP 200 stb.)
      .then(response => {

        // A response objektum tartalmazza a szerver válaszát
        // response.data → a tényleges visszakapott adat (JSON)
        this.users = response.data;

      })

      // Ha hiba történik (pl. nincs internet, 404, 500 stb.)
      .catch(error => {

        // Hiba kiírása a konzolra
        console.error("Hiba történt:", error);

      });
  }
};
```
Async/Await példa:
```js
export default {
  // Reaktív adatok
  data() {
    return {
      users: [] // Ide mentjük a lekért adatokat
    };
  },

  // Az async kulcsszó lehetővé teszi,
  // hogy await-et használjunk a függvényen belül
  async mounted() {

    try {
      // await → megvárja, amíg az axios kérés lefut
      const response = await axios.get(
        "https://jsonplaceholder.typicode.com/users"
      );

      // A sikeres válasz adatának eltárolása
      this.users = response.data;

    } catch (error) {
      // Ha bármi hiba történik a kérés során
      console.error("Hiba történt:", error);
    }
  }
};

```

# POST kérés

A POST kérés új adat létrehozására szolgál.
```js
// POST kérés indítása egy adott API végpontra
axios.post("https://jsonplaceholder.typicode.com/posts", {

  // A második paraméter a küldött adat (request body)
  title: "Teszt cím",
  body: "Ez egy teszt tartalom",
  userId: 1
})

.then(response => {
  // Ha a kérés sikeres (pl. 201 Created)

  // response → a teljes szerver válasz objektum
  // response.data → a szerver által visszaküldött adat (JSON)

  console.log("Sikeres mentés:", response.data);
})

.catch(error => {
  // Ha hiba történik (pl. 400, 500, nincs kapcsolat)
  console.error("Hiba:", error);
});


```

#  PUT és DELETE
### PUT – adat frissítése
```js 
axios.put("https://jsonplaceholder.typicode.com/posts/1", {
  title: "Frissített cím"
})
.then(response => {
  console.log("Frissítve:", response.data);
});
```
### DELETE – adat törlése
```js 
axios.delete("https://jsonplaceholder.typicode.com/posts/1")
.then(() => {
  console.log("Sikeres törlés");
});
```

# Globális konfiguráció

Az Axios globális beállításai módosíthatók.

Base URL beállítása
```js
axios.defaults.baseURL = "https://api.example.com";
```

Alapértelmezett header beállítása:
```js
axios.defaults.headers.common["Authorization"] = "Bearer token";
```

Ezek a beállítások minden kérésre automatikusan érvényesek lesznek.