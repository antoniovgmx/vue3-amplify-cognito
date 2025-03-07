<!-- <template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-card class="pa-5">
          <v-btn color="primary">Click Me</v-btn>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template> -->

<template>
  <v-app id="login" class="secondary">
    <v-main>
      <v-container fluid fill-height>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4" lg="4">
            <v-card class="elevation-1 pa-3">
              <v-card-text>
                <div class="d-flex flex-column align-center">
                  <h1 class="my-4 primary--text">Plataforma de Mantenimiento (ALPHA)</h1>
                </div>
                <v-form>
                  <v-text-field
                    append-inner-icon="mdi-account"
                    label="Login"
                    type="text"
                    v-model="userEmail"
                    :error="error"
                    :rules="[rules.required]"
                  />
                  <v-text-field
                    :type="hidePassword ? 'password' : 'text'"
                    :append-inner-icon="hidePassword ? 'mdi-eye-off' : 'mdi-eye'"
                    label="Password"
                    v-model="password"
                    :error="error"
                    :rules="[rules.required]"
                    @click:append-inner="hidePassword = !hidePassword"
                  />
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn block color="primary" @click="signIn" :loading="loading">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <v-snackbar v-model="showResult" :timeout="2000" location="top">
        {{ result }}
      </v-snackbar>
    </v-main>
  </v-app>
</template>

<!-- <script setup>
  //
</script> -->

<!-- <script>
  import { Auth } from 'aws-amplify';
  import '@/amplify'; // Your AWS config file
    
  export default {
    data() {
      return {
        loading: false,
        userEmail: 'usuario@compañía.com',
        password: 'contraseña',
        hidePassword: true,
        error: false,
        showResult: false,
        result: '',
        rules: {
          required: value => !!value || 'Campo Requerido.'
        }
      }
    },
  
    methods: {
      async signIn() {
        try {
          const user = await Auth.signIn(this.email, this.password);
          console.log('Login successful:', user);
        } catch (error) {
          console.log(error)
          this.errorMessage = error.message;
        }
      },
      // async handleLogin(){
      //   try {
      //     await Auth.signIn(this.username, this.password);
      //     this.$router.push({ name: 'camiones' }); // Redirect to home
      //   } catch (err) {
      //     this.error = err.message || 'An error occurred.';
      //   }
      // },
      login() {
        const vm = this;
  
        if (!vm.userEmail || !vm.password) {
  
          vm.result = "Email y Contraseña no pueden estar vacíos.";
          vm.showResult = true;
  
          return;
        }
  
        if (vm.userEmail === "test" && vm.password === "test") {
          vm.$router.push({ name: 'camiones' });
        }
        else {
          vm.error = true;
          vm.result = "Email o Contraseña son incorrectos.";
          vm.showResult = true;
        }
      }
    }
  }
</script> -->

<script setup>
  import { ref } from 'vue';
  import { Auth } from 'aws-amplify';
  
  const username = ref('');
  const password = ref('');
  
  const signIn = async () => {
    try {
      const user = await Auth.signIn(username.value, password.value);
      console.log('User signed in:', user);
    } catch (error) {
      console.error('Error signing in:', error);
    }
  };
</script>

<style scoped lang="css">
  #login {
    height: 50%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    content: "";
    z-index: 0;
  }
</style>