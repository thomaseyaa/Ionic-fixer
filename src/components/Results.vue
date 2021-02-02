<template>
  <ion-card color="light" class="ion-padding">
    <ion-card-content>
      <ion-title>{{ result }} {{ currency.symbol}}</ion-title>
    </ion-card-content>
  </ion-card>
</template>

<script>
import { IonCard, IonCardContent, IonTitle } from '@ionic/vue';

export default({
  name: "Results",
  components: {
    IonCard,
    IonCardContent,
    IonTitle
  },
  props: ['currency'],
  data(){
    return{
      result: "",
      rate: "",
    }
  },
  methods: {
    convert(){
      fetch(`http://data.fixer.io/api/latest?access_key=${process.env.VUE_APP_API_KEY}&symbols&symbols=${this.currency.symbol}`)
          .then(response => response.json())
          .then(data => {
            this.rate = data.rates[this.currency.symbol]
            this.result = Math.round((this.rate * this.currency.amount) * 100) / 100
          })
          .catch(function (error){
            console.log(error);
          });
    },
  },
  watch: {
    currency: {
      deep: true,
      handler(){
        this.convert();
      }
    }
  },
  mounted(){
    this.convert();
  },
})
</script>