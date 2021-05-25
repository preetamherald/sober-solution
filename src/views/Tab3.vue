<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Know your Solution?</ion-title>
      </ion-toolbar>
      <ion-toolbar>
        <ion-searchbar
          debounce="500"
          :onIonChange="(e) => fetchSearchResults(e.detail.value)"
        ></ion-searchbar>
      </ion-toolbar>
    </ion-header>
    <ion-content v-if="state.loading">
      <div class="center">
        <ion-spinner color="primary"></ion-spinner>
      </div>
    </ion-content>

    <ion-content :fullscreen="true" v-else>
      <div
        class="center"
        v-if="state.searchResults == null || state.searchResults.length == 0"
      >
        <ion-label>No results available, maybe a Treasure 🏴‍☠️</ion-label>
      </div>
      <drink-card
        v-else
        v-for="drink in state.searchResults"
        :key="drink.idDrink"
        :drink="drink"
      ></drink-card>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonSearchbar,
  IonSpinner,
  IonLabel,
} from "@ionic/vue";
import { reactive } from "vue";
import { useRoute, useRouter } from "vue-router";
import axios from "axios";
import IDrinkDetails from "../interfaces/IDrinkDetails";
import DrinkCard from "@/components/DrinkCard.vue";

export default {
  name: "Tab3",
  components: {
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonPage,
    IonSearchbar,
    IonSpinner,
    DrinkCard,
    IonLabel,
  },
  setup() {
    const state = reactive({
      searchResults: [] as IDrinkDetails[],
      loading: true,
    });

    const fetchSearchResults = async (searchTerm: string) => {
      state.loading = true;

      if (searchTerm) {
        state.searchResults = [];
        const res = await axios.get(
          `https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${searchTerm}`
        );

        if (res.data) {
          state.searchResults = res.data?.drinks;
        }
      }
      state.loading = false;
    };

    return {
      state,
      fetchSearchResults,
    };
  },
};
</script>

<style>
.center {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 80vh;
}

ion-spinner {
  transform: scale(1.5);
}
</style>