<template>
  <div class="data-filter">
    <!-- v-model="searchQuery": Kétirányú adat-kötés (Two-way data binding). -->
    <!-- Bármit ír a felhasználó a mezőbe, az automatikusan frissíti a 'searchQuery' változót, és fordítva. -->
    <input
      type="text"
      v-model="searchQuery"
      placeholder="Keresés név alapján..."
    />

    <ul>
      <!-- A ciklus most nem az eredeti 'data' tömbön, hanem a szűrt 'filteredData' tömbön megy végig -->
      <li v-for="item in filteredData" :key="item.id">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script setup>
// A Vue könyvtárból beimportáljuk a szükséges funkciókat:
// ref: Reaktív változó létrehozásához.
// computed: Kiszámított érték generálásához.
// watch: Változások megfigyeléséhez.
import { ref, computed, watch } from "vue";

// A feladatban kapott kiindulási adatok[cite: 2]
const data = [
  { id: 1, name: "John Doe" },
  { id: 2, name: "Jane Doe" },
  { id: 3, name: "Jim Smith" },
  { id: 4, name: "Sarah Johnson" },
];

// A keresőmező aktuális tartalmát tároló reaktív változó (alapértelmezetten üres string)
const searchQuery = ref("");

// computed property: Kiszámított érték[cite: 2].
// Bármikor, ha a 'searchQuery' megváltozik, ez a függvény automatikusan újrafut!
const filteredData = computed(() => {
  return data.filter((item) =>
    // toLowerCase(): Kisbetűssé alakítja a nevet és a keresési kifejezést is, így nem számít a kis/nagybetű (case-insensitive)[cite: 2].
    // includes(): Megnézi, hogy a név tartalmazza-e a beírt keresőszót.
    item.name.toLowerCase().includes(searchQuery.value.toLowerCase()),
  );
});

// watch: Figyeli a 'searchQuery' változót[cite: 2].
// Amikor módosul a keresőmező tartalma, lefut a megadott függvény, és kiírja az új értéket a konzolra[cite: 2].
watch(searchQuery, (newVal) => {
  console.log("Keresési feltétel megváltozott:", newVal);
});
</script>

<style scoped>
input {
  padding: 8px;
  margin-bottom: 10px;
  width: 200px;
}
</style>
