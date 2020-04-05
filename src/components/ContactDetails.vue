<template>
<div>
  <div v-if="!isInEditMode" class="card" style="width: 18rem;">
    <div class="card-body">
      <router-link :to="{name: 'contact', params:{id: contact.id} }">
        <h5 class="card-title">{{ contact.data().lastName }} {{ contact.data().firstName }}</h5>
      </router-link>
      <h6 class="card-subtitle mb-2 text-muted">{{ contact.data().email }}</h6>
      <p class="card-text">Numéro de téléphone: {{contact.data().phone}}.</p>
      <button class="btn btn-sm btn-warning mr-3" @click="editContact">modifier</button>
      <button
      class="btn btn-sm btn-danger"
      @click="$emit('deleteContact', contact)"
      >
      supprimer
      </button>
    </div>
  </div>
  <div v-if="isInEditMode" class="card" style="width: 18rem;">
    <div class="card-body">
      <input v-model="contactClone.lastName" type="text" /><br>
      <input v-model="contactClone.firstName" type="text" /><br>
      <input v-model="contactClone.email" type="text" /><br>
      <input v-model="contactClone.phone" type="text" /><br>
      <button class="btn btn-sm btn-success mr-3" @click="saveEdit">valider la modif</button>
      <button class="btn btn-sm btn-warning" @click="cancelEdit">annuler</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: ['contact'],
  data() {
    return {
      contactClone: {},
      isInEditMode: false,
    };
  },
  methods: {
    editContact() {
      const {
        firstName,
        lastName,
        email,
        phone,
      } = this.contact.data();
      this.contactClone = {
        id: this.contact.id,
        firstName,
        lastName,
        email,
        phone,
      };
      this.isInEditMode = true;
    },
    saveEdit() {
      this.$emit('saveEdit', this.contactClone);
      this.isInEditMode = false;
    },
    cancelEdit() {
      this.isInEditMode = false;
    },
  },
};
</script>

<style scoped></style>
