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

// Charger les données des communes
const { data: listeCommune, error } = await supabase
  .from("commune")
  .select("*");
if (error) console.log("n'a pas pu charger la table Commune :", error);
// Les convertir par `map` en un tableau d'objets {value, label} pour FormKit
const optionsCommune = listeCommune?.map((commune) => ({
  value: commune.commune_code,
  label: commune.commune_nom,
}));

async function supprimerQuartier() {
  const { data, error } = await supabase
    .from("quartier")
    .delete()
    .match({ quartier_code: quartier.value.quartier_code });
  if (error) {
    console.error(
      "Erreur à la suppression de ",
      quartier.value,
      "erreur :",
      error
    );
  } else {
    router.push("/quartier");
  }
}
</script>
    
    <template>
        <div>
            <div class="p-2">
                <FormKit type="form" v-model="quartier" @submit="upsertquartier"
                         :submit-attrs="{classes: { input: 'bg-blue-200 p-1 rounded border border-blue-500 mt-2' }}"
                         :config="{classes: {input: 'border border-gray-500 rounded-sm'}}">
                    <FormKit name="quartier_nom" label="nom du quartier"/>
                    
<!-- Affiche les communes avec comme valeur l'id de la relation -->
                    <FormKit
                      type="select"
                      name="commune_code"
                      label="Commune"
                      :options="optionsCommune"
                    />

                </FormKit>

                <button
                       type="button"
                       v-if="quartier.quartier_code"
                       @click="($refs.dialogSupprimer).showModal()"
                       class="focus-style justify-self-end rounded-md bg-red-500 p-2 shadow-sm mt-2"
                     >
                       Supprimer l'offre
                     </button>
                     <dialog
                       ref="dialogSupprimer"
                       @click="($event.currentTarget).close()"
                     >
                       <button
                         type="button"
                         class="focus-style justify-self-end rounded-md bg-blue-300 p-2 shadow-sm"
                       >
                         Annuler</button
                       ><button
                         type="button"
                         @click="supprimerQuartier()"
                         class="focus-style rounded-md bg-red-500 p-2 shadow-sm"
                       >
                         Confirmer suppression
                       </button>
                     </dialog>
            </div>
        </div>
    </template>