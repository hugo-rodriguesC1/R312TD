<script setup>
import FormulaireCommune from "../../components/FormulaireCommune.vue";

defineProps({ id: String });
</script>
        
        <template>
            <div>
                <FormulaireCommune :id="id"
                />
            </div>
        </template>