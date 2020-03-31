<template>
  <div class="home-view-container">
    <h1>Adopt a new best friend.</h1>
    <p>{{ animalsCount }} animals listed</p>
    <p>{{ getAllCats.length}} cats</p>
    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group id="input-group-1" label="Pet's Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="formData.name"
          required
          placeholder="Enter name"
          type="text"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Species:" label-for="input-2">
        <b-form-select
          id="input-2"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-3" label="Breed:" label-for="input-3">
        <b-form-input
          id="input-3"
          v-model="formData.breed"
          required
          placeholder="Enter breed"
          type="text"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-4" label="Gender:" label-for="input-4">
        <b-form-select
          id="input-4"
          v-model="formData.gender"
          :options="['male', 'female']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-5" label="Pet's Age:" label-for="input-5">
        <b-form-input
          id="input-5"
          v-model="formData.age"
          required
          placeholder="Enter age"
          type="number"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-6" label="Color:" label-for="input-6">
        <b-form-input
          id="input-6"
          v-model="formData.color"
          required
          placeholder="Enter color"
          type="text"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-7" label="Weight:" label-for="input-7">
        <b-form-input
          id="input-7"
          v-model="formData.weight"
          required
          placeholder="Enter weight"
          type="number"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-8" label="Location:" label-for="input-8">
        <b-form-input
          id="input-8"
          v-model="formData.location"
          required
          placeholder="Enter location"
          type="text"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-9" label="Notes:" label-for="input-9">
        <b-form-input
          id="input-9"
          v-model="formData.notes"
          required
          placeholder="Enter notes"
          type="text"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        breed: '',
        color: '',
        gender: '',
        location: '',
        notes: '',
        species: null,
        weight: 0
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, name, age, breed, color, gender, location, notes, weight } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age,
          species,
          breed,
          color,
          gender,
          location,
          notes,
          weight
        }
      }
      this.addPet(payload)

      // reset form after submit
      this.formData = {
        name: '',
        age: 0,
        breed: '',
        color: '',
        gender: '',
        location: '',
        notes: '',
        species: null,
        weight: 0
      }
      this.showPetForm = false
    }
  }
}
</script>
