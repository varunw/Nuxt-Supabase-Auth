<template>
  <div>
    <div class="title">
      <h2>Login</h2>
    </div>
    <div class="container form">
      <label for="uname"><b>Username</b></label>
      <input
        v-model="user.username"
        type="text"
        class="input"
        placeholder="Enter Username"
        name="uname"
        required
      />

      <label for="psw"><b>Password</b></label>
      <input
        v-model="user.password"
        type="password"
        class="input"
        placeholder="Enter Password"
        name="psw"
        required
      />

      <button @click.prevent="signup" class="button">Sign up</button>
      <button @click.prevent="login" class="button">Login</button>
      <h1 v-if="login_bool">Success</h1>
    </div>
  </div>
</template>
<script lang="ts" setup>
import { createClient } from "@supabase/supabase-js";
let signup_bool = ref(false);
let login_bool = ref(false);
const supabase = createClient(
  "https://fszntnhcrmvbtoaojabs.supabase.co",
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImZzem50bmhjcm12YnRvYW9qYWJzIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MDczOTI2OTEsImV4cCI6MjAyMjk2ODY5MX0.nRC5CAXtRu2X5DcFR90NM-PgM5LTF_LMPfbmMg6M9jc"
);
const user = ref({
  username: "",
  password: "",
});

const signup = async () => {
  const { data, error } = await supabase.auth.signUp({
    email: user.value.username,
    password: user.value.password,
  });
  if (error) {
    console.log(error);
    signup_bool.value = false;
  } else {
    console.log(data);
    signup_bool.value = true;
  }

  //   const { data, error } = await supabase.auth.signInWithPassword({
  //     email: user.value.username,
  //     password: user.value.password,
  //   });
  //   if (error) {
  //     console.log(error);
  //     login_bool.value = false;
  //   } else {
  //     console.log(data);
  //     login_bool.value = true;
  //   }
};

const login = async () => {
  const { data, error } = await supabase.auth.signInWithPassword({
    email: user.value.username,
    password: user.value.password,
  });
  if (error) {
    console.log(error);
    login_bool.value = false;
  } else {
    console.log(data.session.access_token);
    login_bool.value = true;
  }
};

//const {data,error} = await supabase.auth.
</script>
