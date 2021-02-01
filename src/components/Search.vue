<template>
  <ion-card>
    <ion-item color="light">
      <ion-label position="stacked">Amount</ion-label>
      <ion-input v-model="convert.amount"></ion-input>
    </ion-item>

    <ion-item color="dark">
      <ion-label>From</ion-label>
      <ion-select interface="action-sheet" value="EUR">
        <ion-select-option value="EUR">EUR</ion-select-option>
      </ion-select>
    </ion-item>

  </ion-card>

  <ion-card>
    <ion-item color="dark">
      <ion-label>To</ion-label>
      <ion-select interface="action-sheet" v-model="convert.symbol" placeholder="USD">
        <ion-select-option v-for="(currencies,name) in currencies" :key="currencies" :value="name">{{ currencies }}</ion-select-option>
      </ion-select>
    </ion-item>
  </ion-card>

  <section>
    <ion-button expand="block" color="success" @click="getValue">Convert</ion-button>
  </section>

  <ion-card v-if="!convert.amount || !convert.symbol" color="danger" class="ion-padding">
    <ion-card-content>
      <h2>Enter an amount and a currency !</h2>
    </ion-card-content>
  </ion-card>
</template>

<script>
import { IonCard, IonItem, IonLabel, IonInput, IonSelect, IonSelectOption, IonButton } from '@ionic/vue';

export default({
  name: 'Home',
  components: {
    IonCard,
    IonItem,
    IonLabel,
    IonInput,
    IonSelect,
    IonSelectOption,
    IonButton,
  },
  data(){
    return{
      currencies: [],
      convert: {
        amount: "",
        symbol: "",
      }
    }
  },
  methods: {
    currenciesList(){
      fetch(`http://data.fixer.io/api/symbols?access_key=${process.env.VUE_APP_API_KEY}`)
      .then(response => response.json())
      .then(data => {
        console.log(data);
        this.currencies = data.symbols;
      })
      .catch(function (error) {
        console.log(error)
      })
    },
    getValue(){
      this.$emit('amount', this.convert)
    },
  },
  mounted(){
    this.currenciesList();
  }
});
</script>

<style scoped>
section:not(.full-width),
.full-width > header{
  padding: 0 14px;
}
h2{
  text-align: center;
}
</style>