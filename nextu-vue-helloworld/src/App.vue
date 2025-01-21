<template>
  <div id="app">
    <div class="container">
      <h1>Formulaire d'inscription</h1>
      <form @submit.prevent="validateForm">
        
        <div>
          <label for="nom">Nom:</label>
          <input type="text" id="nom" v-model="form.nom" />
          <span v-if="errors.nom" class="error">{{ errors.nom }}</span>
        </div>

        <div>
          <label for="prenom">Prénom:</label>
          <input type="text" id="prenom" v-model="form.prenom" />
          <span v-if="errors.prenom" class="error">{{ errors.prenom }}</span>
        </div>

        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="form.email" />
          <span v-if="errors.email" class="error">{{ errors.email }}</span>
        </div>

        <div>
          <label>Sexe:</label>
          <label>
            <input type="radio" value="Homme" v-model="form.sexe" /> Homme
          </label>
          <label>
            <input type="radio" value="Femme" v-model="form.sexe" /> Femme
          </label>
          <span v-if="errors.sexe" class="error">{{ errors.sexe }}</span>
        </div>

        <div>
          <label for="adresse">Adresse:</label>
          <input type="text" id="adresse" v-model="form.adresse" />
          <span v-if="errors.adresse" class="error">{{ errors.adresse }}</span>
        </div>

        <div>
          <label for="codePostal">Code postal:</label>
          <input type="text" id="codePostal" v-model="form.codePostal" />
          <span v-if="errors.codePostal" class="error">{{ errors.codePostal }}</span>
        </div>

        <div>
          <label for="ville">Ville:</label>
          <input type="text" id="ville" v-model="form.ville" />
          <span v-if="errors.ville" class="error">{{ errors.ville }}</span>
        </div>

        <div>
          <label for="institut">Nom de l'institut:</label>
          <input type="text" id="institut" v-model="form.institut" />
          <span v-if="errors.institut" class="error">{{ errors.institut }}</span>
        </div>

        <div class="buttons">
          <button type="submit">Valider</button>
          <button type="button" @click="resetForm">Annuler</button>
        </div>
      </form>

      <div v-if="formSubmitted">
        <h2>Données soumises :</h2>
        <div class="fiche">
          <p><strong>Nom :</strong> {{ submittedData.nom }}</p>
          <p><strong>Prénom :</strong> {{ submittedData.prenom }}</p>
          <p><strong>Email :</strong> {{ submittedData.email }}</p>
          <p><strong>Sexe :</strong> {{ submittedData.sexe }}</p>
          <p><strong>Adresse :</strong> {{ submittedData.adresse }}</p>
          <p><strong>Code Postal :</strong> {{ submittedData.codePostal }}</p>
          <p><strong>Ville :</strong> {{ submittedData.ville }}</p>
          <p><strong>Institut :</strong> {{ submittedData.institut }}</p>
        </div>
      </div>
    </div>

    <div v-if="showPopup" class="popup">
      <div class="popup-content">
        <p>Formulaire envoyé avec succès</p>
        <button @click="closePopup">Fermer</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        nom: '',
        prenom: '',
        email: '',
        sexe: '',
        adresse: '',
        codePostal: '',
        ville: '',
        institut: '',
      },
      errors: {
        nom: null,
        prenom: null,
        email: null,
        sexe: null,
        adresse: null,
        codePostal: null,
        ville: null,
        institut: null,
      },
      formSubmitted: false,
      submittedData: {},
      showPopup: false,
    };
  },
  methods: {
    validateForm() {
      this.errors = {
        nom: null,
        prenom: null,
        email: null,
        sexe: null,
        adresse: null,
        codePostal: null,
        ville: null,
        institut: null,
      };

      let isValid = true;

      if (!this.form.nom) {
        this.errors.nom = 'Le champ Nom est requis.';
        isValid = false;
      }

      if (!this.form.prenom) {
        this.errors.prenom = 'Le champ Prénom est requis.';
        isValid = false;
      }

      const emailRegex = /^[^\s@]+@[^\s@]+\.[a-z]{2,}$/i;
      if (!this.form.email) {
        this.errors.email = 'Le champ Email est requis.';
        isValid = false;
      } else if (!emailRegex.test(this.form.email)) {
        this.errors.email = 'Veuillez saisir un email valide.';
        isValid = false;
      }

      if (!this.form.sexe) {
        this.errors.sexe = 'Veuillez sélectionner un sexe.';
        isValid = false;
      }

      if (!this.form.adresse) {
        this.errors.adresse = 'Le champ Adresse est requis.';
        isValid = false;
      }

      const codePostalRegex = /^[0-9]{5}$/;
      if (!this.form.codePostal) {
        this.errors.codePostal = 'Le champ Code postal est requis.';
        isValid = false;
      } else if (!codePostalRegex.test(this.form.codePostal)) {
        this.errors.codePostal = 'Le Code postal doit être composé de 5 chiffres.';
        isValid = false;
      }

      if (!this.form.ville) {
        this.errors.ville = 'Le champ Ville est requis.';
        isValid = false;
      }

      if (!this.form.institut) {
        this.errors.institut = 'Le champ Institut est requis.';
        isValid = false;
      }

      if (isValid) {
        this.submittedData = { ...this.form };
        this.formSubmitted = true;
        this.showPopup = true;
        this.resetForm();
      }
    },

    resetForm() {
      this.form = {
        nom: '',
        prenom: '',
        email: '',
        sexe: '',
        adresse: '',
        codePostal: '',
        ville: '',
        institut: '',
      };
      this.errors = {
        nom: null,
        prenom: null,
        email: null,
        sexe: null,
        adresse: null,
        codePostal: null,
        ville: null,
        institut: null,
      };
      this.formSubmitted = false;
    },

    closePopup() {
      this.showPopup = false;
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: auto;
  padding: 20px;
  border: 1px solid rgba(214, 214, 214, 0.2);
  border-radius: 5px;
  background-color: #f9f9f9;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 4px 8px rgba(214, 214, 214, 0.2);
}

form {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

form div {
  flex: 1 1 calc(50% - 20px);
  display: flex;
  flex-direction: column;
}

form div.full-width {
  flex: 1 1 100%;
}

label {
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.error {
  margin-top: 5px;
  color: red;
  font-size: 12px;
}

.buttons {
  flex: 1 1 100%;
  display: flex;
  gap: 10px;
  justify-content: flex-end;
}

button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
  font-size: 14px;
}

button[type="button"] {
  background-color: #ccc;
}

button:hover {
  background-color: #0056b3;
}

button[type="button"]:hover {
  background-color: #999;
}

.popup {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.popup-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
}

.popup button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.popup button:hover {
  background-color: #0056b3;
}

.fiche {
  padding: 10px;
  background-color: #e9ecef;
  border-radius: 5px;
}
</style>


<!--exo1 jour1
 <template>
  <div id="app">
    <product-list :products="products" />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import AsideView from './components/layouts/AsideView.vue'
import HeaderView from './components/layouts/HeaderView.vue'
import NavView from './components/layouts/NavView.vue'
import HomeProjectView from './views/HomeProjectView.vue'

export default {
  name: 'App',
  components: {
    ProductList,
  },
  data() {
    return {
      products: [
        { id: 1, label: 'Carotte', description: 'De belles carottes', qte: 10 },
        { id: 2, label: 'Pomme', description: 'Des pommes vertes', qte: 0 },
        { id: 3, label: 'Tomate', description: 'Tomates rouges', qte: 5 },
      ],
    };
  },
};
</script>

<style>
</style>  -->