<script setup>
import Card from "../components/card.vue";
import maisons from "../assets/maisons.json";
</script>
            
        <template>
            <div>
                <div class="p-2">Page liste avec données JSON</div>
            </div>
            <div v-for="maison in maisons" :key="maison.id">
                <Card v-bind="maison"/>
            </div>
    
    
        </template>
        
        