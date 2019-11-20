
<template>
  <v-container>
     <img src="../assets/ics.png" style="height:100px;width:75px" />
     <v-btn color="transparent" height="40" width="110" >TENTANG ICS</v-btn>
     <v-btn color="transparent" height="40" width="110" >DIVISI</v-btn>
     <v-btn color="transparent" height="40" width="110" >EVENT</v-btn>
     <v-btn color="transparent" height="40" width="110" >MATERI</v-btn>
     <v-btn color="pink" height="40" width="110" >REGISTRASI</v-btn>
     <v-btn color="light blue" height="40" width="110" >LOGIN</v-btn>
    <v-card>

 
        <v-card-actions class="justify-center">
        </v-card-actions>
        <h1 class="text-md-center">LOGIN</h1>
        <v-layout row wrap style="margin:10px" justify="center">
          <v-row>
            <v-col cols="12">
              <v-text-field label="Email*" v-model="form.email" required></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field label="Password*" v-model="form.password" type="password" required></v-text-field>
            </v-col>
            <v-btn @click="login()" block color="green" height="40" width="10">LOGIN</v-btn>
          </v-row>
        </v-layout>

    </v-card>

  </v-container>
</template>



<script>
export default {
  data() {
    return {
      snackbar: false,
      color: null,
      text: "",
      load: false,
      form: {
        email: "",
        password: ""
      },
      user: new FormData()
    };
  },
  methods: {
    login() {
      var url = this.$apiUrl + "/Auth";

      this.user = new FormData();
      this.user.append("email", this.form.email);
      this.user.append("password", this.form.password);

      this.$http.post(url, this.user).then(response => {
        if (response.data.token) {
          localStorage.setItem("token", response.data.token);
          this.$router.push({ name: "UserController" });
        } else {
          this.snackbar = true;
          this.text = "Invalid Username or Password!";
          this.color = "red";
          this.load = false;
        }
      });
    }
  }
};
</script>
