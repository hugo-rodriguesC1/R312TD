<script setup>
import Card from "../components/card.vue";
</script>
    
<template>
    <div>
        <div class="p-2">Page simple</div>

    </div>
    <Card :price="2700"
            name="Beverly Springfield"
            adress="2821 Lake Sevilla, Palm Harbor, TX"
            :nb="4"
            :nsdb="2"
            surface="6x7.5"
            image="/src/assets/img1.jpg"/>
</template>

