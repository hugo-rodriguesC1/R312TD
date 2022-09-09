<script setup>
const res = await fetch("/public/maisons.json");
const maisons = await res.json();

import Card from "../components/card.vue";
</script>
            
<template>
            <Card v-for="maison in maisons" :key="maison.id" v-bind="maison"/>
       
</template>
        
        