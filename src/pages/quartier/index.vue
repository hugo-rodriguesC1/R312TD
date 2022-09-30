<script setup>
import { supabase } from "../../supabase";
import groupBy from "lodash/groupBy";
import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";

const { data, error } = await supabase.from("allquartier").select("*");
if (error) console.log("n'a pas pu charger la table quartiercommune :", error);
</script>
    
    <template>
      <section class="flex flex-col">
        <h3 class="text-2xl">Liste des quartiers</h3>
        <ul>
          <li v-for="quartierObject in (data)" :key="quartierObject.id">
            {{ quartierObject.commune_nom }} -
            {{ quartierObject.quartier_nom }}
          </li>
        </ul>
        <br>

        <h3>Disclosure</h3>
        <Disclosure v-for="(listeQuartier, Commune_nom) in groupBy(data,'commune_nom')" :key="Commune_nom">
            <DisclosureButton>{{Commune_nom}}</DisclosureButton>
            <DisclosurePanel>
                <li
                    v-for="quartierObject in listeQuartier"
                    :key="quartierObject.code_Quartier"
                >{{quartierObject.quartier_nom}}</li>
            </DisclosurePanel>
        </Disclosure>
      </section>
    </template>