<script setup>
import Card from "./card.vue";

import { ref } from "@vue/reactivity";
import { useRouter } from "vue-router";
import { supabase } from "../supabase";
const router = useRouter();

let maison = ref();

const props = defineProps(["id"]);

if (props.id) {
  // On charge les données de la maison
  let { data, error } = await supabase
    .from("maison")
    .select("*")
    .eq("maison_code", props.id);
  if (error) console.log("n'a pas pu charger le table Maison :", error);
  else maison.value = data[0];
}

async function upsertMaison(dataForm, node) {
  const { data, error } = await supabase.from("maison").upsert(dataForm);
  if (error) node.setErrors([error.message]);
  else {
    node.setErrors([]);
    router.push({
      name: "edit-id",
      params: { id: data[0].maison_code },
    });
  }
}
</script>

<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">Résultat (Prévisualisation)</h2>
            <Card v-bind="maison" class="max-w-md"/>
        </div>
        <div class="p-2">
            <FormKit type="form" v-model="maison" @submit="upsertMaison"
                     :submit-attrs="{classes: { input: 'bg-blue-200 p-1 rounded border border-blue-500' }}"
                     :config="{classes: {input: 'border border-gray-500 rounded-sm'}}
                     
                     ">
                <FormKit name="name" label="nom" />
                <FormKit name="adress" label="adresse" />
                <FormKit name="price" label="prix" type="number" />
                <FormKit name="nb" label="nombre de chambres" type="number" />
                <FormKit name="nsdb" label="nombre de salles de bain" type="number" />
                <FormKit name="surface" label="surface" />
                <FormKit name="favoris" label="mettre en valeur" type="checkbox" wrapper-class="flex my-4 gap-2"/>
            </FormKit>
        </div>
    </div>
</template>