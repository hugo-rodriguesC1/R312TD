<script setup>
import FormulaireQuartier from "../../components/FormulaireQuartier.vue";

defineProps({ id: String });
</script>
        
        <template>
            <div>
                <FormulaireQuartier :id="id"
                />
            </div>
        </template>