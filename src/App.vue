<template>
  <div id="app">
    <nav class="navbar navbar-expand navbar-dark bg-dark">
      <router-link to="/" class="navbar-brand">Front SpringBoot App</router-link>
      <div class="navbar-nav mr-auto">
        <li class="nav-item">
          <router-link to="/" class="nav-link">Personnes</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/ajouter-personne" class="nav-link">Ajouter</router-link>
        </li>
      </div>
    </nav>

    <div class="container-lg">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: "app"
};
</script>
