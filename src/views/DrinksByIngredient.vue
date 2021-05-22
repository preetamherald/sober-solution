<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-button slot="start">
          <ion-back-button></ion-back-button>
        </ion-button>
        <ion-title>{{ ingredient }} Drinks</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content v-if="state.loading">
      <div class="loading-center">
        <ion-spinner color="primary"></ion-spinner>
      </div>
    </ion-content>
    <ion-content :fullscreen="true" v-else>
      <ion-list>
        <ion-item
          v-for="drink in state.lstDrinks"
          :key="drink.idDrink"
          @click="() => router.push(`/drinks/${drink.idDrink}`)"
        >
          <ion-avatar slot="start">
            <img :src="drink.strDrinkThumb" />
          </ion-avatar>
          <ion-label>
            <h2>
              {{ drink.strDrink }}
            </h2>
          </ion-label>
        </ion-item>
      </ion-list>
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
  IonList,
  IonItem,
  IonLabel,
  IonSpinner,
  IonAvatar,
  IonButton,
  IonBackButton,
} from "@ionic/vue";
import { reactive } from "vue";
import { useRouter, useRoute } from "vue-router";
import axios from "axios";

interface Drink {
  strDrink: string;
  strDrinkThumb: string;
  idDrink: string;
}

export default {
  name: "DrinksByIngredient",
  components: {
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonPage,
    IonList,
    IonItem,
    IonLabel,
    IonSpinner,
    IonAvatar,
    IonButton,
    IonBackButton,
  },

  setup() {
    const router = useRouter();
    const route = useRoute();

    const ingredient = route.params.ingredient as string;

    const state = reactive({
      lstDrinks: [] as Drink[],
      loading: false,
    });

    const fetchDrinkByIngredient = async (ingredient: string) => {
      state.loading = true;

      const res = await axios.get(
        `https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=${ingredient}`
      );

      if (res.data) {
        state.lstDrinks = res.data?.drinks;
      }
      state.loading = false;
    };

    fetchDrinkByIngredient(ingredient);

    return {
      router,
      state,
      ingredient,
    };
  },
};
</script>

<style>
.loading-center {
  display: flex;
  align-content: center;
  justify-content: center;
  height: 90vh;
}

ion-spinner {
  transform: scale(1.5);
}
</style>