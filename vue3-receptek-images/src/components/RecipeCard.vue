<template>
<div class='card'>
  <img :src='recept.kep' class='img'/>
  <h3>{{ recept.nev }}</h3>
  <button @click='$emit("details", recept)'>Részletek</button>
</div>
</template>

<script setup>
defineProps({ recept:Object })
</script>

<style>
.card{background:#fff;border-radius:6px;padding:10px;box-shadow:0 0 5px #0003;}
.img{width:100%;height:160px;object-fit:cover;border-radius:6px;}
button{margin-top:10px;padding:6px 10px;}
</style>
