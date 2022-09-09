<script setup>
import Card from "../components/card.vue";
import maisons from "../assets/maisons.json";

defineProps({ nbr: String });
</script>
            
        <template>
            <div>
                <div class="p-2">Page liste avec routes dynamiques</div>
            </div>
                <Card v-bind="maisons[nbr]"/>

    
    
        </template>
        
        