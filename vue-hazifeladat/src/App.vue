<template>
  <!-- A template rész tartalmazza azt a HTML struktúrát, ami megjelenik a képernyőn -->
  <div style="padding: 20px; font-family: sans-serif">
    <h2>1. Feladat: MainNavigation</h2>
    <!-- Így illesztjük be az beimportált MainNavigation komponenst -->
    <MainNavigation />

    <hr style="margin: 30px 0" />

    <h2>2. Feladat: DataFilter</h2>
    <!-- Így illesztjük be a DataFilter komponenst -->
    <DataFilter />

    <hr style="margin: 30px 0" />

    <h2>3. Feladat: UserForm</h2>
    <!-- Így illesztjük be a UserForm komponenst -->
    <UserForm />
  </div>
</template>

<script setup>
// A <script setup> a Vue 3 legmodernebb szintaxisa.
// Itt importáljuk be a 'components' mappából az általunk készített 3 különálló komponenst.
import MainNavigation from "./components/MainNavigation.vue";
import DataFilter from "./components/DataFilter.vue";
import UserForm from "./components/UserForm.vue";
</script>
