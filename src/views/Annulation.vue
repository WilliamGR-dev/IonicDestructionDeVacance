<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Reservation</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Reservation</ion-title>
        </ion-toolbar>
      </ion-header>
      <h1 style="text-align: center">
        Diteco RDV
      </h1>

      <ion-card>
        <h1>Annulation</h1>
        <ion-item>
          <ion-label>Id Reservation</ion-label>
          <ion-input v-model="form.token" name="token" type="token"   placeholder="Token"></ion-input>
        </ion-item>
        <ion-item>
          <ion-label>Confirmation d'annulation</ion-label>
          <ion-checkbox v-model="form.validate" name="validate" ></ion-checkbox>
        </ion-item>
        <ion-button type="sumbit" color="primary" v-on:click="onSumbit">Annuler</ion-button>
      </ion-card>


    </ion-content>
  </ion-page>
</template>

<script>
  import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonInput, IonCheckbox, IonLabel, IonItem, IonButton } from '@ionic/vue';

  export default  {
    data() {
      return {
        form: {
          validate: false,
          token: "",
        }
      }
    },
    name: 'Reservation',
    components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonCard, IonInput, IonCheckbox, IonLabel, IonItem, IonButton},
    methods: {


      onSumbit() {

        fetch(`https://destructiondevac.herokuapp.com/api/booking/${this.form.token}`, {
          method: 'POST',
          mode: 'no-cors',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded;charset=UTF-8'
          },
          body: new URLSearchParams(this.form)
        }).then(function(response) {
          console.log(response);
        }).catch(console.error)


      }

    },
  }
</script>