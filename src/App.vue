<template>
  <nav>
    <h4 class="text-xl">
      menu (dans <code class="font-mono">/src/App.vue</code>)
    </h4>
    <ul>
      <li>
        <router-link class="text-red-600 underline" to="/">
          lien vers
          <code class="font-mono">/src/pages/index.vue</code>
        </router-link>
      </li>
      <li>
        <router-link class="text-red-600 underline" to="/simple">
          lien vers
          <code class="font-mono">simple</code>
        </router-link>
      </li>
      <li>
        <router-link class="text-red-600 underline" to="/liste">
          lien vers
          <code class="font-mono">liste</code>
        </router-link>
      </li>
      <li>
        <router-link class="text-red-600 underline" to="/listeJson">
          lien vers
          <code class="font-mono">liste avec fichier JSON</code>
        </router-link>
      </li>
      <li>
        <router-link class="text-red-600 underline" to="/liste-fetch">
          lien vers
          <code class="font-mono">liste avec fetch</code>
        </router-link>
      </li>
      <li>
        <router-link class="text-red-600 underline" to="/edit/new">
          lien vers
          <code class="font-mono">formulaire</code>
        </router-link>
      </li>
      <li>
        <router-link class="text-red-600 underline" to="/liste-supabase">
          lien vers
          <code class="font-mono">liste supabase</code>
        </router-link>
      </li>
      <li>
        <router-link class="text-red-600 underline" to="/connexion">
          lien vers
          <code class="font-mono">connexion</code>
        </router-link>
      </li>
    </ul>
  </nav>

  <!-- Affiche les pages -->
  <Suspense>
        <template #default>
          <router-view class="m-2 border-2 p-2" />
        </template>
        <template #fallback>
            Loading...
        </template>
    </Suspense>
</template>

<script setup lang="ts">
</script>
