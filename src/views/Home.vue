<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title class="ion-text-center">Diteco</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Diteco</ion-title>
        </ion-toolbar>
      </ion-header>

      <IonCard>
        <img src="https://diteco.fr/bg.jpg" />
        <h1 class="display-4 fw-normal text-white ion-text-center">Reservation RDV</h1>
      </IonCard>

      <ion-card style="text-align: center">
        Diteco aide les particuliers à effectuer leur transition énergétique depuis 2 ans. Chaque particulier est accompagné du début et même après que l'installation est terminé. L'objectif de Diteco est toujours le même qui est de proposé une énergie qui respecte l'environnement.
      </ion-card>

      <ion-card>Horaires</ion-card>

      <ion-card class="table-responsive">
        <ion-grid class="table">
          <ion-row>
            <ion-col scope="col" v-for="day in information['weekDay']" :key="day">{{ day }}</ion-col>
          </ion-row>
          <ion-row>
            <ion-col>{{ information['hours_min'] }}h - {{ information['hours_max'] }}h</ion-col>
            <ion-col>{{ information['hours_min'] }}h - {{ information['hours_max'] }}h</ion-col>
            <ion-col>{{ information['hours_min'] }}h - {{ information['hours_max'] }}h</ion-col>
            <ion-col>{{ information['hours_min'] }}h - {{ information['hours_max'] }}h</ion-col>
            <ion-col>{{ information['hours_min'] }}h - {{ information['hours_max'] }}h</ion-col>
            <ion-col class="text-muted"><em>Fermé</em></ion-col>
            <ion-col  class="text-muted"><em>Fermé</em></ion-col>
          </ion-row>
        </ion-grid>
      </ion-card>

      <ion-card>Informations pratiques</ion-card>

    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonCol, IonRow, IonGrid } from '@ionic/vue';

export default  {
  data() {
    return {
      information: {
        hours_min: "",
        hours_max: "",
        weekDay: [],
      },
    }
  },
  name: 'Home',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonCard, IonCol, IonRow, IonGrid },


  mounted() {
    fetch(`https://destructiondevac.herokuapp.com/api/infos`).then((response)=>{
      response.json().then((data)=> {
        console.log(data.reservation);
        if (data.length !== 0){
          this.information.hours_max = data.reservation.hours_max;
          this.information.hours_min = data.reservation.hours_min;
          this.information.weekDay = data.reservation.jours;
        }
      });
    });
  }
}
</script>