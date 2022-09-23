<script setup>
import { supabase } from "../supabase";
import Card from "../components/card.vue";

console.log("supabase :", supabase); // pour vérifier et "garder" supabase dans le code

let { data: maison, error } = await supabase.from("maison").select("*");
console.log("maison :", maison);
const maisons = maison; // à remplacer par l'appel à Supabase
console.log(maisons);
</script>
            
<template>
            <Card v-for="maison in maisons" :key="maison.id" v-bind="maison"/>
       
</template>
        
        