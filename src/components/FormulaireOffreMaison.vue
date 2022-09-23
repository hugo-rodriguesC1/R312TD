<script setup>
import { ref } from "@vue/reactivity";
import Card from "./card.vue";
import { useRouter } from "vue-router";
import { supabase } from "../supabase";
const router = useRouter();

const props = defineProps({ idMaison: Number });

let { data: maison, error } = await supabase
  .from("maison")
  .select("*")
  .eq("id", props.idMaison);
if (error) console.log("n'a pas pu charger le table Maison :", error);
const maisons = maison; // à remplacer par l'appel à Supabase

async function upsertMaison(dataForm, node) {
  const { data, error } = await supabase.from("maison").upsert(dataForm);
  if (error) node.setErrors([error.message]);
}
</script>

<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">Résultat (Prévisualisation)</h2>
            <Card v-bind="maison[0]" class="max-w-md"/>
        </div>
        <div class="p-2">
            <FormKit type="form" v-model="maison[0]" @submit="upsertMaison"
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