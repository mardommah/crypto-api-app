<template>
  <ion-content>
    <div class="button">
      <ion-button @click="exchangeRate()">Get Data</ion-button>
    </div>
    <ion-grid>
  <ion-row v-for="crypt in exchangeResult.data" :key="crypt.id">
    <!-- First Section -->
    <ion-col size="4">
      <!-- Your content for the first section goes here -->
      <div>Rank</div>
      <div class="details">{{ crypt.rank }}</div>
    </ion-col>

    <!-- Second Section -->
    <ion-col size="4">
      <!-- Your content for the second section goes here -->
      <div class="properties">{{ crypt.name }}</div>
      <div class="details">{{ crypt.symbol }}</div>
    </ion-col>

    <!-- Third Section -->
    <ion-col size="4">
      <!-- Your content for the third section goes here -->
      <div class="properties">USD</div>
      <div class="details">{{ crypt.price_usd }}</div>
    </ion-col>
  </ion-row>
</ion-grid>
<pre>{{ exchangeResult }}</pre>
</ion-content>
</template>

<script setup lang="ts">
import { IonPage, IonContent, IonCol, IonGrid, IonRow } from '@ionic/vue';
import { ref, onMounted, defineComponent } from 'vue';
import axios from 'axios';

const exchangeResult = ref()

const exchangeRate = async () =>{
  await axios('https://api.coinlore.net/api/tickers/')
    .then(response =>{
      exchangeResult.value = response.data
      console.log(response)
    })
}

onMounted(async () => await exchangeRate())

</script>

<style scoped>
  *{
    margin-left: auto;
    margin-right: auto;
  }
  ion-col{
    border: solid 1px #fff;
    color: #fff;
    text-align: center;
  }
  .details{
    margin-top: 20px;
    font-size: 25px;
  }

  .ion-button{
    justify-content: center;
  }

  .button{
    position: relative;
    display: block;
    width: 100px;
    margin-top: 20px;
    margin-bottom: 50px;
  }

</style>