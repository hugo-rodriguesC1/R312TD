<script setup>
import Card from "../components/card.vue";
const maisons = [
  {
    price: 2700,
    name: "Palm Harbor",
    adress: "2699 Green Valley, Highland Lake",
    nb: 3,
    nsdb: 3,
    surface: "7x8",
    image: "/src/assets/img2.jpg",
  },
  {
    price: 2700,
    name: "Faulkner Ave",
    adress: "909 Woodland St, Michigan, IN",
    nb: 3,
    nsdb: 2,
    surface: "7x10",
    image: "/src/assets/img3.jpg",
  },
  {
    price: 2700,
    name: "St. Christal",
    adress: "210 US Highway, HighlandLake, FL",
    nb: 5,
    nsdb: 5,
    surface: "6x8,5",
    image: "/src/assets/img4.jpg",
  },
];
</script>
        
    <template>
        <div>
            <div class="p-2">Page liste avec données JSON</div>
        </div>
        <div v-for="maison in maisons" :key="maison.id">
            <Card v-bind="maison"/>
        </div>


    </template>
    
    