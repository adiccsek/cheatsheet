```html 
<template>
  <div>
    <h1>Ingatlanok</h1>

    <!-- 🔹 Új ingatlan felvitel -->
    <div>
      <input v-model="ujIngatlan.leiras" placeholder="Leírás" />
      <input v-model="ujIngatlan.kepUrl" placeholder="Kép URL" />
      <button @click="createIngatlan">Mentés</button>
    </div>

    <hr />

    <!-- 🔹 Lista megjelenítése -->
    <div v-for="ingatlan in ingatlanok" :key="ingatlan.id">
      <h3>{{ ingatlan.leiras }}</h3>
      <img :src="ingatlan.kepUrl" width="200" />
      <p>Dátum: {{ ingatlan.hirdetesDatuma }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      // 🔹 Itt tároljuk a GET-ből kapott adatokat
      ingatlanok: [],

      // 🔹 Ez az objektum megy POST-tal a backendnek
      ujIngatlan: {
        kategoriaId: 1,
        leiras: "",
        hirdetesDatuma: new Date().toISOString(),
        tehermentes: true,
        kepUrl: ""
      }
    };
  },

  mounted() {
    // Betöltéskor lekérjük az adatokat
    this.fetchIngatlanok();
  },

  methods: {
    
    // 🔹 GET kérés
    async fetchIngatlanok() {
      try {
        const response = await axios.get("http://localhost:8080/api/ujingatlan");

        // 👉 Itt dolgozzuk fel a response-t
        // response.data tartalmazza a backend JSON válaszát
        this.ingatlanok = response.data;

      } catch (error) {
        console.error("GET hiba:", error);
      }
    },

    // 🔹 POST kérés
    
    async createIngatlan() {
      try {
        const response = await axios.post(
          "http://localhost:8080/api/ujingatlan",
          this.ujIngatlan
        );

        console.log("Mentve:", response.data);

        // Mentés után újra lekérjük a listát
        await this.fetchIngatlanok();

        // Űrlap ürítése
        this.ujIngatlan.leiras = "";
        this.ujIngatlan.kepUrl = "";

      } catch (error) {
        console.error("POST hiba:", error);
      }
    }

  }
};
</script>

```