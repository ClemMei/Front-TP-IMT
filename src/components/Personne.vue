<template>
  <!-- A COMPLETER -->
  <div class="container">
    <div class="submit-form">
      <div v-if="currentPersonne">
        <input
          class="form-control"
          type="text"
          id="name"
          required
          v-model="currentPersonne.name"
          name="name"
          placeholder="Nom"
        /><br />
        <input
          class="form-control"
          type="text"
          id="surname"
          required
          v-model="currentPersonne.surname"
          name="surname"
          placeholder="Prénom"
        /><br />
        <input
          class="form-control"
          type="text"
          id="phone"
          required
          v-model="currentPersonne.phone"
          name="phone"
          placeholder="Téléphone"
        /><br />
        <input
          class="form-control"
          type="text"
          id="city"
          required
          v-model="currentPersonne.city"
          name="city"
          placeholder="Ville"
        /><br />

        <!-- A INCLURE DANS LE FORM -->
        <button class="badge badge-danger mr-2" @click="deletePersonne">
          Supprimer
        </button>

        <!-- A INCLURE DANS LE FORM -->

        <button
          type="submit"
          class="badge badge-success"
          @click="updatePersonne"
        >
          Modifier
        </button>
        <p><br />{{ message }}</p>
      </div>

      <div v-else>
        <div class="alert alert-danger alert-dismissible fade show text-center" >
          <strong>Error!</strong> <br />Cette personne n'existe pas, veuillez
          <a href="http://localhost:8081/">retourner à l'accueil</a>
        </div>
        <p>
          <br />
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personne",
  data() {
    return {
      currentPersonne: null,
      message: "",
    };
  },
  methods: {
    getPersonne(id) {
      // A COMPLETER
      PersonneDataService.get(id)
        .then((response) => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    updatePersonne() {
      // A COMPLETER
      PersonneDataService.update(this.currentPersonne)
        .then((response) => {
          this.message = "Personne modifiée avec succès!";
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    deletePersonne() {
      // A COMPLETER
      PersonneDataService.delete(this.currentPersonne.id)
        .then((response) => {
          this.$router.push({ name: "personnes" });
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
  mounted() {
    this.message = "";
    this.getPersonne(this.$route.params.id);
  },
};
</script>

<style>
.edit-form {
  max-width: 300px;
  margin: auto;
}
</style>
