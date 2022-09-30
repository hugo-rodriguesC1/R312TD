<script setup>
import { ref } from "@vue/reactivity";
import { useRouter } from "vue-router";
import { supabase } from "../supabase";
const router = useRouter();

let commune = ref();

const props = defineProps(["id"]);

if (props.id) {
  // On charge les données de la maison
  let { data, error } = await supabase
    .from("commune")
    .select("*")
    .eq("commune_code", props.id);
  if (error) console.log("n'a pas pu charger le table commune :", error);
  else commune.value = data[0];
}

async function upsertcommune(dataForm, node) {
  const { data, error } = await supabase.from("commune").upsert(dataForm);
  if (error) node.setErrors([error.message]);
  else {
    node.setErrors([]);
    router.push({
      name: "commune-id",
      params: { id: data[0].commune_code },
    });
  }
}
</script>
        
        <template>
            <div>
                <div class="p-2">
                    <FormKit type="form" v-model="commune" @submit="upsertcommune"
                             :submit-attrs="{classes: { input: 'bg-blue-200 p-1 rounded border border-blue-500 mt-2' }}"
                             :config="{classes: {input: 'border border-gray-500 rounded-sm'}}">
                        <FormKit name="commune_nom" label="nom de la commune"/>
                        <FormKit name="commune_distance" label="distance de l'agence"/>
    
                    </FormKit>
                </div>
            </div>
        </template>