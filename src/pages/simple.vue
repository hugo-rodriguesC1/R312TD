<script setup>
import Card from "../components/card.vue";
let maison = {
  price: 2700,
  name: "Palm Harbor",
  adress: "2699 Green Valley, Highland Lake",
  nb: 3,
  nsdb: 3,
  surface: "7x8",
  image: "/src/assets/img2.jpg",
};
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
    <Card v-bind="maison"/>
</template>

