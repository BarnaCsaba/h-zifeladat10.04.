<template>
  <!-- @submit.prevent="submitForm": Az űrlap elküldésekor megakadályozza a böngésző alapértelmezett oldal-újratöltését (preventDefault)[cite: 3], és helyette meghívja a 'submitForm' függvényt. -->
  <form @submit.prevent="submitForm">
    <!-- User Name Mező -->
    <div class="form-group">
      <label for="username">Username:</label>
      <input type="text" id="username" v-model="username" />
      <!-- v-if="hasUsernameError": Csak akkor jelenik meg ez a <p> bekezdés a HTML-ben, ha a 'hasUsernameError' értéke true (tehát van hiba)[cite: 2]. -->
      <p v-if="hasUsernameError" class="error">
        Username must be at least 5 characters long and different from password
      </p>
    </div>

    <!-- Password Mező -->
    <div class="form-group">
      <label for="password">Password:</label>
      <input type="password" id="password" v-model="password" />
      <p v-if="hasPasswordError" class="error">
        Password must be at least 8 characters long and different from username
      </p>
    </div>

    <!-- Confirm Password Mező -->
    <div class="form-group">
      <label for="confirmPassword">Confirm Password:</label>
      <input type="password" id="confirmPassword" v-model="confirmPassword" />
      <p v-if="hasConfirmPasswordError" class="error">
        Confirm password must be at least 8 characters long and match with
        password
      </p>
    </div>

    <button type="submit">Küldés</button>
  </form>
</template>

<script setup>
import { ref, computed } from "vue";

// Reaktív változók az űrlap mezőinek adatstátuszához (alapértelmezetten mind üres string)
const username = ref("");
const password = ref("");
const confirmPassword = ref("");

// Computed property-k a validációhoz: azonnal kiértékelődnek a betöltődéskor is[cite: 2]

// Username hibás, ha: 5 karakternél rövidebb VAGY megegyezik a jelszóval (amennyiben a username nem üres)[cite: 2]
const hasUsernameError = computed(() => {
  return (
    username.value.length < 5 ||
    (username.value !== "" && username.value === password.value)
  );
});

// Password hibás, ha: 8 karakternél rövidebb VAGY megegyezik a felhasználónévvel (amennyiben a jelszó nem üres)[cite: 2]
const hasPasswordError = computed(() => {
  return (
    password.value.length < 8 ||
    (password.value !== "" && password.value === username.value)
  );
});

// ConfirmPassword hibás, ha: 8 karakternél rövidebb VAGY nem egyezik meg a megadott jelszóval[cite: 2]
const hasConfirmPasswordError = computed(() => {
  return (
    confirmPassword.value.length < 8 || confirmPassword.value !== password.value
  );
});

// A gomb megnyomásakor lefutó függvény
const submitForm = () => {
  // Ellenőrizzük, hogy egyik mezőnél sincs-e hiba (! azt jelenti, hogy NOT / NEM)
  if (
    !hasUsernameError.value &&
    !hasPasswordError.value &&
    !hasConfirmPasswordError.value
  ) {
    // Ha nincs hiba, feldobunk egy figyelmeztető (alert) ablakot a megadott adatokkal[cite: 3]
    alert(
      `Adatok:\nFelhasználónév: ${username.value}\nJelszó: ${password.value}\nJelszó megerősítve: ${confirmPassword.value}`,
    );

    // Visszaállítjuk a mezők kezdőértékét üresre[cite: 3]
    username.value = "";
    password.value = "";
    confirmPassword.value = "";
  }
};
</script>

<style scoped>
.form-group {
  margin-bottom: 1.5rem;
  display: flex;
  flex-direction: column;
  width: 300px;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
}

input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.error {
  color: red; /* Piros hibaüzenet */
  margin-top: 0.3rem;
  font-size: 0.85rem;
}

button {
  padding: 10px 15px;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #33a06f;
}
</style>
