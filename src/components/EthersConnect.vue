<script setup lang="ts">
import { ethers } from "ethers";
import { ref } from "vue";

let signerAddr = ref('')

async function connectWallet() {
const provider = new ethers.providers.Web3Provider((window as any).ethereum)
console.log(provider)
await provider.send("eth_requestAccounts", []);
const signer = provider.getSigner()

signerAddr.value = await signer.getAddress()
}

</script>

<template>

<button @click="connectWallet">Connect using ethers</button>
<p>Signer is {{ signerAddr }}</p>

</template>