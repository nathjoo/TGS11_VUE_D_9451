<template>
  <v-app>
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="8" md="8">
            <v-card>
              <v-row cols="6">
                <v-col>
                  <div class="header">
                    <div id="title">
                      Login
                    </div>
                    <div id="tagline">

                    </div>
                  </div>
                  <div class="form">
                    <v-text-field v-model="form.email" label="Email" outlined height=50></v-text-field>
                    <v-text-field v-model="form.password" type="password" label="Password" outlined height=50></v-text-field>
                    <v-btn @click="login()" id="buton" height=50 block color="green" class="elevation-0">Login</v-btn>
                  </div>
                </v-col>
                <v-col cols="6" md="6" style="padding:0px">
                  <v-img :src="require('@/assets/jo.jpg')"></v-img>
                </v-col>
              </v-row>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>


<script>
  export default {
    data() {
      return {
        form: {
          email: '',
          password: '',
        },
        user: new FormData,
      }
    },
    methods: {
      login() {
        var url = this.$apiUrl + '/auth'
        this.user = new FormData()
        this.user.append('email', this.form.email);
        this.user.append('password', this.form.password);
        this.$http.post(url, this.user).then(response => {
          if (response.data.token) {
            localStorage.setItem("token", response.data.token)
            this.$router.push({
              name: "UserController"
            })
          } else {
            alert('gagal login')
          }
        })

      }
    }
  }
</script>

<style>
  .header {
    margin-top: 1px;
  }

  #tagline {
    font-family: roboto;
    font-style: normal;
    font-weight: normal;
    font-size: 20px;
    text-align: center;
  }

  #title {
    font-family: ribeye;
    font-style: normal;
    font-weight: normal;
    font-size: 40px;
    text-align: center;
  }

  .form {
    margin-left: 80px;
    margin-right: 80px;
    margin-top: 130px;
    margin-bottom: 50px;
  }
</style>