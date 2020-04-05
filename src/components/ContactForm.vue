<template>
    <div>
<h2>CONTACT FORM</h2>

<form @submit.prevent="createContact">
    <input type="text" name="" id="" placeholder="prénom" v-model="contact.firstName"><br>
    <input type="text" name="" id="" placeholder="nom" v-model="contact.lastName"><br>
    <input type="text" name="" id="" placeholder="email" v-model="contact.email"><br>
    <input type="text" name="" id="" placeholder="tel"  v-model="contact.phone"><br>
    <button type="submit">Soumettre</button>
</form>
    </div>
</template>

<script>
import db from '../shared/db';

export default {
  data() {
    return {
      contact: {
        firstName: '',
        lastName: '',
        email: '',
        phone: '',
      },
    };
  },
  methods: {
    createContact() {
      db.create(this.contact)
        .then((data) => {
          console.log(data);
          this.$emit('created');
          this.resetForm();
        })
        .catch((error) => console.log(error));
    },
    resetForm() {
      this.contact.firstName = '';
      this.contact.lastName = '';
      this.contact.email = '';
      this.contact.phone = '';
    },
  },
};

</script>

<style lang="scss" scoped>

</style>
