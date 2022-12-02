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
    <v-row>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Pregnancies"
          placeholder="Agrega el Campo"
          v-model="newElement[['Pregnancies']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Glucose"
          placeholder="Agrega el Campo"
          v-model="newElement[['Glucose']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="BloodPresure"
          placeholder="Agrega el Campo"
          v-model="newElement[['BloodPresure']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="SkinThickness"
          placeholder="Agrega el Campo"
          v-model="newElement[['SkinThickness']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Insulin"
          placeholder="Agrega el Campo"
          v-model="newElement[['Insulin']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="BMI"
          placeholder="Agrega el Campo"
          v-model="newElement[['BMI']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="DiabetesPedigreeFunction"
          placeholder="Agrega el Campo"
          v-model="newElement[['DiabetesPedigreeFunction']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Age"
          placeholder="Agrega el Campo"
          v-model="newElement[['Age']]"
        />
      </v-col>
      <v-col cols="9" style="margin: auto">
        <v-text-field
          type="number"
          label="Outcome"
          placeholder="Agrega el Campo"
          v-model="newElement[['Outcome']]"
        />
      </v-col>
      <v-col cols="12" style="text-align: center">
        <v-btn v-on:click="newData()"> Enviar Información </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "indexComponent",

  data: () => ({
    measureValue: "",
    measure: false,
    toSend: {},
    newElement: {},
  }),

  methods: {
    entrenarModelo() {
      axios
        .post("http://54.160.150.74:8080/api/model-database/model", {})
        .then((response) => {
          console.log(response.data);
        });
    },

    sendNewData() {
      axios
        .post(
          "http://54.160.150.74:8080/api/model-database/model-prediction",
          this.toSend
        )
        .then((response) => {
          console.log(response.data);
        });
    },

    newData() {
      axios
        .post(
          "http://54.160.150.74:8080/api/model-database/registro",
          this.newElement
        )
        .then((response) => {
          console.log(response.data);
        });
    },
  },
};
</script>
