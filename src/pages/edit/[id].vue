<script setup>
import FormulaireOffreMaison from "../../components/FormulaireOffreMaison.vue";
import { supabase } from "../../supabase";

defineProps({ id: Number });

let { data: maison, error } = await supabase.from("maison").select("*");
const maisons = maison; // à remplacer par l'appel à Supabase
</script>
    
    <template>
        <div>
            <FormulaireOffreMaison :idMaison=id
            />
        </div>
    </template>