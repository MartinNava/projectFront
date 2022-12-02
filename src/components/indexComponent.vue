<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <p class="title">Modelo de inteligencia artificial mediante Joblib</p>
      </v-col>
    </v-row>
    <v-row>
      <v-col
        cols="12"
        :md="measure ? '6' : '12'"
        class="flexContainer"
        style="text-align: center"
      >
        <v-btn v-on:click="entrenarModelo()"> Reentrenar Modelo </v-btn>
      </v-col>
      <v-col cols="12" md="6" v-if="measure">
        <p>
          {{ measureValue }}
        </p>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="9">
        <p class="subtitle">
          Una vez descubierto tu resultado ayudanos a mejorar poniéndolo
        </p>
        <div class="subtitleDelimiter" />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Pregnancies"
          placeholder="Agrega el Campo"
          v-model="toSend[['Pregnancies']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Glucose"
          placeholder="Agrega el Campo"
          v-model="toSend[['Glucose']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="BloodPresure"
          placeholder="Agrega el Campo"
          v-model="toSend[['BloodPresure']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="SkinThickness"
          placeholder="Agrega el Campo"
          v-model="toSend[['SkinThickness']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Insulin"
          placeholder="Agrega el Campo"
          v-model="toSend[['Insulin']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="BMI"
          placeholder="Agrega el Campo"
          v-model="toSend[['BMI']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="DiabetesPedigreeFunction"
          placeholder="Agrega el Campo"
          v-model="toSend[['DiabetesPedigreeFunction']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Age"
          placeholder="Agrega el Campo"
          v-model="toSend[['Age']]"
        />
      </v-col>
      <v-col cols="12" style="text-align: center">
        <v-btn v-on:click="sendNewData()"> Enviar Información </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "indexComponent",

  data: () => ({
    measureValue: "",
    measure: false,
    toSend: {},
  }),

  methods: {
    entrenarModelo() {
      fetch("http://54.160.150.74:8080/api/model-database/model", {
        method: "POST",
        body: JSON.stringify(this.toSend),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          "Access-Control-Max-Age": 600,
        },
      })
        .then((response) => {
          response.json();
        })
        .then((json) => {
          console.log(json);
        })
        .catch((error) => {
          console.log(error);
        });
    },

    sendNewData() {
      fetch("http://54.160.150.74:8080/api/model-database/model-prediction", {
        method: "POST",
        body: JSON.stringify(this.toSend),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          "Access-Control-Max-Age": 600,
        },
      })
        .then((response) => {
          response.json();
        })
        .then((json) => {
          console.log(json);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
<style>
.title {
  text-align: center;
  font-size: 40pt;
  font-weight: bold;
  margin: 35pt 0;
  z-index: 2;
  position: relative;
}

.subtitle {
  text-align: justify;
  font-weight: bold;
  font-size: 24px;
  margin-top: 15pt;
}

.subtitleDelimiter {
  width: 65px;
  height: 3pt;
  background: #3bb3c1;
  margin-top: -5px;
  margin-bottom: 15pt;
}
</style>