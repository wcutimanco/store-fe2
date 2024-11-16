<template>
  <q-layout>
    <q-page-container>
      <q-page class="flex flex-center q-pa-md" style="height: 100vh">
        <q-card-section>
          <h5>Inicio de sesión</h5>
        </q-card-section>
        <q-card-section>
          <q-input
            v-model="emailValue"
            standout="bg-teal text-white"
            label="Email"
            outlined
            dense
          />
          <q-input
            v-model="pwdValue"
            standout="bg-teal text-white"
            label="Password"
            outlined
            dense
          />
        </q-card-section>
        <q-card-section>
          <q-btn label="login" color="primary" @click="inicioSesion"></q-btn>
        </q-card-section>
      </q-page>
    </q-page-container>
  </q-layout>
</template>
<style></style>
<script>
export default {
  name: "LoginForm",
  data() {
    return {
      emailValue: "",
      pwdValue: "",
    };
  },
  methods: {
    inicioSesion() {
      console.log("Click en el boton de inicio de sesion");
      console.log("Valor de email: " + this.emailValue);

      let endpointLogin = "/api/User/SignIn";
      let user = { email: this.emailValue, password: this.pwdValue };
      this.$api
        .post(endpointLogin, user)
        .then((response) => {
          //Respuesta exitosa
          console.log("Respuesta exitosa: " + JSON.stringify(response));
          this.$router.push("/"); //Esta linea redirecciona a la pagina raiz
        })
        .catch((error) => {
          //Ocurrio un error
          console.log("Error en: " + error);
        });
    },
  },
};
</script>
