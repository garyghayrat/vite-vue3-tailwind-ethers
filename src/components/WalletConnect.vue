<script setup lang="ts">
import { onMounted, ref } from 'vue';

const MetamaskInstalled= ref(false)
let account = ref('');
let isLoggedIn = ref(false);

onMounted(() => {
      console.log("mounted")
      MetamaskInstalled.value = typeof (window as any).ethereum !== 'undefined'
      console.log(MetamaskInstalled.value)
})

async function connectWallet(){
      console.log('button clicked');
      const accounts = await (window as any).ethereum.request({ method: 'eth_requestAccounts' });
      account.value = accounts[0];
      isLoggedIn.value = true;
}

</script>

<template>
<div v-if="!isLoggedIn">
  <button v-if="MetamaskInstalled" @click="connectWallet">Connect Wallet</button>
  <p v-else>Install Metamask</p>
</div>

<div v-if="isLoggedIn">
  <p>Your Account is {{ account }}</p>
</div>

</template>