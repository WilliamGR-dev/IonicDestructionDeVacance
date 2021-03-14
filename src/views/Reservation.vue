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
        <h1>Réservation</h1>
        <div> Réserver une place pour une heure (2 places par heure disponibles).</div>
          <ion-item>
            <ion-label>Email</ion-label>
            <ion-input v-model="form.email" name="email" type="email"   placeholder="Entrer un mail"></ion-input>
          </ion-item>
          <ion-item>
            <ion-label>Date</ion-label>
            <ion-datetime v-model="form.date" name="date" display-format="YYYY-MMM-DD" picker-format="YYYY-MMM-DD"  placeholder="Entrer une date"></ion-datetime>
          </ion-item>
          <ion-item>
            <ion-label>Heures</ion-label>
            <ion-datetime v-model="form.hour" name="hour" display-format="H:mm" picker-format="H:mm" placeholder="Entrer une heure"></ion-datetime>
          </ion-item>
          <ion-item>
            <ion-label>CGU</ion-label>
            <ion-checkbox v-model="form.cgu" name="cgu" ></ion-checkbox>
          </ion-item>
          <ion-button type="sumbit" color="primary" v-on:click="onSumbit">Reserver</ion-button>
      </ion-card>


    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonInput, IonCheckbox, IonLabel, IonItem, IonDatetime, IonButton } from '@ionic/vue';

export default  {
  data() {
    return {
      form: {
        email: "",
        date:"",
        hour:"",
        cgu: false,
      },
    }
  },
  name: 'Reservation',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonCard, IonInput, IonCheckbox, IonLabel, IonItem, IonDatetime, IonButton},
  methods: {


    onSumbit() {
      let newHour = new Date(this.form.hour);
      let newDate = new Date(this.form.date);
      let newMounth = newDate.getMonth()+1;
      console.log(newHour);
      console.log();

      let newForm = {
        ...this.form, ///Destration operator
        hour : `${newHour.getHours().toString().padStart(2,'0')}:${newHour.getMinutes().toString().padStart(2,'0')}`,
        date : `${newDate.getFullYear()}-${newMounth.toString().padStart(2,'0')}-${newDate.getDate().toString().padStart(2,'0')}`,
      };
      console.log(newForm);

      fetch('https://destructiondevac.herokuapp.com/api/booking', {
        method: 'POST',
        mode: 'no-cors',
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded;charset=UTF-8'
        },
        body: new URLSearchParams(newForm)
      }).then(function(response) {
        console.log(response);
      }).catch(console.error)


      }

  },
}
</script>