<template>
  <v-app>
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>


<script setup>
  import { Authenticator } from '@aws-amplify/ui-vue';
  import '@aws-amplify/ui-vue/styles.css';

  import { Amplify } from 'aws-amplify';
  import awsconfig from './aws-exports';

  Amplify.configure(awsconfig);
</script>