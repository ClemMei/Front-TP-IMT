<template>
  <div class="submit-form">
    <div v-if="!submitted">
      <!-- A COMPLETER -->
      <input
        class="form-control"
        type="text"
        id="name"
        required
        v-model="personne.name"
        name="name"
        placeholder="Nom"
      /><br />
      <input
        class="form-control"
        type="text"
        id="surname"
        required
        v-model="personne.surname"
        name="surname"
        placeholder="Prénom"
      /><br />
      <input
        class="form-control"
        type="text"
        id="phone"
        required
        v-model="personne.phone"
        name="phone"
        placeholder="Téléphone"
      /><br />
      <input
        class="form-control"
        type="text"
        id="city"
        required
        v-model="personne.city"
        name="city"
        placeholder="Ville"
      /><br />

      <button @click="creerPersonne" class="btn btn-success">Ajouter</button>
    </div>

    <div v-else>
      <h4>Personne ajoutée avec succès!</h4>
      <button class="btn btn-success" @click="resetForm">
        Ajouter une nouvelle personne
      </button>
    </div>
  </div>
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "add-personne",
  data() {
    return {
      personne: {
        id: null,
        name: "",
        surname: "",
        phone: "",
        city: "",
      },
      submitted: false,
    };
  },
  methods: {
    creerPersonne() {
      var data = {
        id: this.personne.id,
        // A COMPLETER
        name: this.personne.name,
        surname: this.personne.surname,
        phone: this.personne.phone,
        city: this.personne.city,
      };

      // A COMPLETER
      PersonneDataService.create(data)
        .then((response) => {
          console.log(response.data);
          this.submitted = true;
        })
        .catch((e) => {
          console.log(e);
        });
    },

    resetForm() {
      this.submitted = false;
      this.personne = {};
    },
  },
};
</script>

<style>
.submit-form {
  max-width: 300px;
  margin: auto;
}
</style>
