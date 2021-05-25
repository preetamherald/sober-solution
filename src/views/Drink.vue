<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-button slot="start">
          <ion-back-button></ion-back-button>
        </ion-button>
        <ion-title>Sober Solution</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content v-if="state.loading">
      <div class="loading-center">
        <ion-spinner></ion-spinner>
      </div>
    </ion-content>
    <ion-content :fullscreen="true" v-else>
      <drink-card :drink="state.drink" />
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
  IonButton,
  IonBackButton,
} from "@ionic/vue";
import { reactive } from "vue";
import { useRoute, useRouter } from "vue-router";
import axios from "axios";
import DrinkCard from "@/components/DrinkCard.vue";
import IDrinkDetails from "../interfaces/IDrinkDetails";

export default {
  name: "Drink",
  components: {
    DrinkCard,
    IonPage,
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonButton,
    IonBackButton,
  },
  setup() {
    const route = useRoute();

    const drinkId = route.params.id as string;

    const state = reactive({
      drink: {} as IDrinkDetails,
      loading: false,
    });

    const fetchDrinkById = async (drinkId: string) => {
      state.loading = true;

      const res = await axios.get(
        `https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i=${drinkId}`
      );

      if (res.data) {
        state.drink = res.data?.drinks[0];
        state.loading = false;
      }
    };
    fetchDrinkById(drinkId);

    return {
      state,
    };
  },
};
</script>