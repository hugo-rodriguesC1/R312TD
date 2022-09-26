<script setup>
import heart from "./icones/heart.vue";
import dimension from "./icones/dimension.vue";
import bath from "./icones/bath.vue";
import bed from "./icones/bed.vue";
const properties = defineProps({
  maison_code: String,
  price: Number,
  favoris: {
    type: Boolean,
    default: false,
  },
  name: String,
  adress: String,
  nb: Number,
  nsdb: Number,
  surface: String,
  image: String,
});
</script>

<template>
  <figure class="mb-6 mx-4">
    <img class="rounded-t-lg" :src="image" alt="Image maison" />
    <figcaption
      class="relative flex flex-col rounded-b-lg border-2 border-t-0 px-5 py-7"
    >
      <h3 class="text-2xl font-semibold leading-8 text-gray-900">
        {{name}}
      </h3>
      <address class="not-italic text-gray-500">
        {{adress}}
      </address>
      <div class="-order-1 flex items-center">
        <div class="text-2xl text-indigo-500">
          <!-- ${{ price.toLocaleString("en-US") }} -->
          {{price}}
        </div>
        <div class="text-gray-500">/months</div>
      </div>
      <hr class="my-2 border-t-2 border-indigo-100" />
      <div class="flex justify-between text-sm font-normal">
        <div><bed class="inline-block align-top" />{{nb}} Beds</div>
        <div><bath class="inline-block align-top" />{{nsdb}} Bathrooms</div>
        <div><dimension class="inline-block align-top" /> {{surface}} m²</div>
      </div>
      <div
        class="
          absolute
          top-0
          right-0
          grid
          h-12
          w-12
          place-items-center
          rounded-full
          border-2 border-indigo-100
        "
      >
        <heart
          v-on:click="favoris = !favoris"
          :class="{ 'fill-red-400': favoris }"
        />
      </div>
    </figcaption>
  </figure>
</template>

