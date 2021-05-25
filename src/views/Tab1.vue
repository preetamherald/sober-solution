<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Sober Solution</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content v-if="state.loading">
      <div class="loading-center">
        <ion-spinner></ion-spinner>
      </div>
    </ion-content>
    <ion-content :fullscreen="true" v-else>
      <ion-refresher slot="fixed" @ionRefresh="doRefresh">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>
      <drink-card :drink="state.randomCocktail" />
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
  IonRefresher,
  IonSpinner,
  IonRefresherContent,
} from "@ionic/vue";
import { reactive } from "vue";
import axios from "axios";
import DrinkCard from "@/components/DrinkCard.vue";

export default {
  name: "Tab1",
  components: {
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonPage,
    IonRefresher,
    IonSpinner,
    IonRefresherContent,
    DrinkCard,
  },
  setup() {
    const state = reactive({
      randomCocktail: {},
      loading: false,
    });

    const fetchRandomCocktail = async (dispLoaderPage: boolean) => {
      if (dispLoaderPage) {
        state.loading = true;
      }

      const res = await axios.get(
        "https://thecocktaildb.com/api/json/v1/1/random.php"
      );

      if (res.data) {
        state.randomCocktail = res.data?.drinks[0];
      }

      state.loading = false;
    };

    const doRefresh = (event: CustomEvent) => {
      fetchRandomCocktail(false);

      //@ts-expect-error
      event.target?.complete();
    };

    fetchRandomCocktail(true);

    return {
      state,
      fetchRandomCocktail,
      doRefresh,
    };
  },
};
</script>

<style>
.loading-center {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 90vh;
}

ion-spinner {
  transform: scale(1.5);
}
</style>