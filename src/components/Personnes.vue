<template>
  <div class="container">
    <div class="row justify-content-evenly">
      <div class="col">
        <div class="card text-center shadow p-3 mb-5 bg-body rounded">
          <div class="card-body">
            <ul class="list-group">
              <li
                class="list-group-item"
                :class="{ active: id == currentIndex }"
                v-for="(personne, id) in personnes"
                :key="id"
                @click="setActivePersonne(personne, id)"
              >
                {{ personne.surname }} {{ personne.name }}
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="col">
        <div class="card text-center shadow p-3 mb-5 bg-body rounded">
          <div class="card-body">
            <div v-if="currentPersonne">
              {{ currentPersonne.surname }}<br />
              {{ currentPersonne.name }}<br />
              {{ currentPersonne.phone }}<br />
              {{ currentPersonne.city }}<br />
              <router-link
                :to="'/personnes/' + currentPersonne.id"
                class="badge badge-warning"
                >Modifier</router-link
              >
            </div>
            <div v-else>
              <br />
              <p>Cliquez sur une des personnes pour afficher les détails.</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personnes",
  data() {
    return {
      personnes: [],
      currentPersonne: null,
      currentIndex: -1,
    };
  },
  methods: {
    getPersonnes() {
      PersonneDataService.getAll()
        .then((response) => {
          this.personnes = response.data;
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    setActivePersonne(personne, index) {
      this.currentPersonne = personne;
      this.currentIndex = personne ? index : -1;
    },
  },
  mounted() {
    this.getPersonnes();
  },
};
</script>
