<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="success">
        <ion-title class="title">Currency converter</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <div id="container">
        <img src="assets/img/currencies.png"/>
          <Search @amount="getValue"></Search>
          <Results v-if="currency" :currency="currency"></Results>
      </div>
    </ion-content>

    <ion-footer>
      <ion-toolbar color="success">
        <ion-title>Powered by Ionic-fixer</ion-title>
      </ion-toolbar>
    </ion-footer>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonFooter } from '@ionic/vue';
import Search from "@/components/Search.vue";
import Results from "@/components/Results.vue";

export default({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonFooter,
    Search,
    Results
  },
  data(){
    return {
      currency: null,
    }
  },
  methods: {
    getValue(data){
      this.currency = data
    }
  },
});
</script>

<style scoped>
img{
  width: 100px;
  height: 100px;
  display: block;
  margin-right: auto;
  margin-left: auto;
  margin-top: 20px;
}
</style>