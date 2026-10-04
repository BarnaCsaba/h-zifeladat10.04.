<template>
  <!-- <nav> egy HTML5 elem, ami a navigációs sávot jelöli -->
  <nav class="main-navigation">
    <ul class="nav-list">
      <!-- v-for: Ciklus a Vue-ban. Végigmegy a 'menu' tömb elemein. -->
      <!-- :key="index": A Vue-nak szüksége van egy egyedi azonosítóra minden ciklusfejlécnél a gyors frissítéshez. -->
      <li v-for="(item, index) in menu" :key="index" class="nav-item">
        <!-- :href="item.url" -> A kettőspont (v-bind rövidítése) azt jelenti, hogy a 'href' attribútum értéke egy JavaScript változóból jön -->
        <!-- {{ item.text }} -> A dupla kapcsos zárójel (interpolation) írja ki a JavaScript objektum 'text' mezőjét -->
        <a :href="item.url" class="nav-link">{{ item.text }}</a>
      </li>
    </ul>
  </nav>
</template>

<script setup>
// Definiáljuk a menüelemeket tartalmazó tömböt a kért adatszerkezettel[cite: 1]
const menu = [
  { text: "Vue.js", url: "https://vuejs.org/" },
  { text: "React", url: "https://reactjs.org/" },
  { text: "Angular", url: "https://angular.io/" },
  { text: "Svelte", url: "https://svelte.dev/" },
];
</script>

<style scoped>
/* A 'scoped' kulcsszó garantálja, hogy ezek a CSS stílusok CSAK ebben a komponensben fejtik ki hatásukat */
.main-navigation {
  background-color: #333; /* Sötétszürke háttér */
  padding: 1rem; /* Belső margó */
  border-radius: 8px; /* Lekerekített sarkok */
}

.nav-list {
  display: flex; /* Flexbox elrendezés, hogy az elemek egymás mellett (egy sorban) legyenek */
  list-style-type: none; /* Bogyók eltávolítása a listáról */
  margin: 0;
  padding: 0;
  justify-content: center; /* Elemek középre rendezése horizontalisan */
  gap: 2rem; /* Távolság a menüpontok között */
}

.nav-link {
  color: white; /* Fehér szövegszín */
  text-decoration: none; /* Aláhúzás eltávolítása a linkről */
  font-weight: bold; /* Félkövér betűtípus */
}

/* :hover -> Amikor az egérrel a link fölé visszük a kurzort */
.nav-link:hover {
  color: #42b883; /* Vue zöld színre vált */
}
</style>
