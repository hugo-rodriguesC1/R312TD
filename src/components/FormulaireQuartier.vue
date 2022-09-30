<script setup>
import { ref } from "@vue/reactivity";
import { useRouter } from "vue-router";
import { supabase } from "../supabase";
const router = useRouter();

let quartier = ref();

const props = defineProps(["id"]);

if (props.id) {
  // On charge les données de la maison
  let { data, error } = await supabase
    .from("quartier")
    .select("*")
    .eq("quartier_code", props.id);
  if (error) console.log("n'a pas pu charger le table quartier :", error);
  else quartier.value = data[0];
}

async function upsertquartier(dataForm, node) {
  const { data, error } = await supabase.from("quartier").upsert(dataForm);
  if (error) node.setErrors([error.message]);
  else {
    node.setErrors([]);
    router.push({
      name: "quartier-id",
      params: { id: data[0].quartier_code },
    });
  }
}
</script>
    
    <template>
        <div>
            <div class="p-2">
                <FormKit type="form" v-model="quartier" @submit="upsertquartier"
                         :submit-attrs="{classes: { input: 'bg-blue-200 p-1 rounded border border-blue-500' }}"
                         :config="{classes: {input: 'border border-gray-500 rounded-sm'}}
                         
                         ">
                    <FormKit name="quartier_nom" label="nom" />

                </FormKit>
            </div>
        </div>
    </template>