<template>
  <div id="app">
    <ContactForm @created="getAllContacts" />
    <ContactList
    :contacts="contacts"
    @deleteContact="deleteContact"
    @saveEdit="saveEdit"
    />
    <router-view/>
  </div>
</template>

<script>
import ContactList from '@/components/ContactList.vue';
import ContactForm from '@/components/ContactForm.vue';
import db from '../shared/db';

export default {
  data() {
    return {
      contacts: [],
    };
  },
  name: 'App',
  components: {
    ContactForm,
    ContactList,
  },
  created() {
    this.getAllContacts();
  },
  methods: {
    deleteContact(contact) {
      db.delete(contact.id).then(() => {
        this.getAllContacts();
      }).catch((error) => console.log(error));
    },
    saveEdit(editedContact) {
      db.update(editedContact).then(() => {
        this.getAllContacts();
      }).catch((error) => { console.log(error); });
    },
    getAllContacts() {
      db.read()
        .then((snapchot) => {
          console.log(snapchot);
          this.contacts = snapchot.docs;
        })
        .catch((error) => console.error(error));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
