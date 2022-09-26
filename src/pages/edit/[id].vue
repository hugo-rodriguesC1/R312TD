<script setup>
import FormulaireOffreMaison from "../../components/FormulaireOffreMaison.vue";
import { ref } from "vue";
import { supabase } from "../../supabase";
let maison = ref();

defineProps({ id: String });
</script>
    
    <template>
        <div>
            <FormulaireOffreMaison :id="id"
            />
        </div>
    </template>