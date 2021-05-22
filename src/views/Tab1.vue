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
      <ion-card>
        <img :src="state.randomCocktail.strDrinkThumb" />
        <ion-card-header>
          <ion-card-subtitle>
            {{ state.randomCocktail.strCategory }} | served in
            {{ state.randomCocktail.strGlass }}
          </ion-card-subtitle>
          <ion-card-title>
            {{ state.randomCocktail.strDrink }}
          </ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <p>{{ state.randomCocktail.strInstructions }}</p>
          <ion-list-header> Ingredients </ion-list-header>
          <ion-list>
            <ion-item v-if="state.randomCocktail.strIngredient1">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure1">
                  {{ state.randomCocktail.strMeasure1 }} -
                </span>
                {{ state.randomCocktail.strIngredient1 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient2">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure2">
                  {{ state.randomCocktail.strMeasure2 }} -
                </span>
                {{ state.randomCocktail.strIngredient2 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient3">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure3">
                  {{ state.randomCocktail.strMeasure3 }} -
                </span>
                {{ state.randomCocktail.strIngredient3 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient4">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure4">
                  {{ state.randomCocktail.strMeasure4 }} -
                </span>
                {{ state.randomCocktail.strIngredient4 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient5">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure5">
                  {{ state.randomCocktail.strMeasure5 }} -
                </span>
                {{ state.randomCocktail.strIngredient5 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient6">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure6">
                  {{ state.randomCocktail.strMeasure6 }} -
                </span>
                {{ state.randomCocktail.strIngredient6 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient7">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure7">
                  {{ state.randomCocktail.strMeasure7 }} -
                </span>
                {{ state.randomCocktail.strIngredient7 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient8">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure8">
                  {{ state.randomCocktail.strMeasure8 }} -
                </span>
                {{ state.randomCocktail.strIngredient8 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient9">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure9">
                  {{ state.randomCocktail.strMeasure9 }} -
                </span>
                {{ state.randomCocktail.strIngredient9 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient10">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure10">
                  {{ state.randomCocktail.strMeasure10 }} -
                </span>
                {{ state.randomCocktail.strIngredient10 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient11">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure11">
                  {{ state.randomCocktail.strMeasure11 }} -
                </span>
                {{ state.randomCocktail.strIngredient11 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient12">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure12">
                  {{ state.randomCocktail.strMeasure12 }} -
                </span>
                {{ state.randomCocktail.strIngredient12 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient13">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure13">
                  {{ state.randomCocktail.strMeasure13 }} -
                </span>
                {{ state.randomCocktail.strIngredient13 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient14">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure14">
                  {{ state.randomCocktail.strMeasure14 }} -
                </span>
                {{ state.randomCocktail.strIngredient14 }}
              </ion-label>
            </ion-item>
            <ion-item v-if="state.randomCocktail.strIngredient15">
              <ion-label>
                <span v-if="state.randomCocktail.strMeasure15">
                  {{ state.randomCocktail.strMeasure15 }} -
                </span>
                {{ state.randomCocktail.strIngredient15 }}
              </ion-label>
            </ion-item>
          </ion-list>
        </ion-card-content>
      </ion-card>
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
  IonCard,
  IonCardContent,
  IonList,
  IonItem,
  IonLabel,
  IonListHeader,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonRefresherContent,
} from "@ionic/vue";
import { reactive } from "vue";
import axios from "axios";

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
    IonCard,
    IonCardContent,
    IonList,
    IonItem,
    IonLabel,
    IonListHeader,
    IonCardHeader,
    IonCardTitle,
    IonCardSubtitle,
    IonRefresherContent,
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
  align-content: center;
  justify-content: center;
  height: 90vh;
}

ion-spinner {
  transform: scale(1.5);
}
</style>