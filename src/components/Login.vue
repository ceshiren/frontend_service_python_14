<template>
  <v-app id="inspire">
    <v-main>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <v-card class="elevation-12">
              <v-toolbar color="primary" dark flat>
                <v-toolbar-title>Login form</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-tooltip bottom>
                  <template v-slot:activator="{ on }">
                    <v-btn :href="source" icon large target="_blank" v-on="on">
                      <v-icon>mdi-code-tags</v-icon>
                    </v-btn>
                  </template>
                  <span>Source</span>
                </v-tooltip>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field
                    v-model="username"
                    label="Login"
                    name="login"
                    prepend-icon="mdi-account"
                    type="text"
                  ></v-text-field>

                  <v-text-field
                    v-model="password"
                    id="password"
                    label="Password"
                    name="password"
                    prepend-icon="mdi-lock"
                    type="password"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click="login">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import http from "@/http";

export default {
  name: "Login",
  props: {
    source: String,
  },
  methods: {
    login: function () {
      console.log(this);
      console.log(this.username);
      console.log(this.password);
      http
        .post("/login", {
          username: this.username,
          password: this.password,
        })
        .then((res) => {
          console.log(res);
          if (res.data.errcode === 0) {
            //如果errcode=0 就把正确结果的token保存到localStorage中
            localStorage.setItem("token", res.data.token);
            console.log(localStorage.getItem("token"));
            this.$router.push("dashboard");
          } else {
            //alert error
            window.alert("username or passowrd error");
          }
        });
    },
  },
};
</script>