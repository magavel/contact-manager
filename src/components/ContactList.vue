<template>
  <div class="auto">
    <contact-details
      class="m-3"
      :contact="contact"
      v-for="contact in contacts"
      :key="contact.data().id"
      @saveEdit="saveEdit"
      @deleteContact="deleteContact"
      ></contact-details>
  </div>
</template>

<script>
import ContactDetails from '@/components/ContactDetails.vue';

export default {

  props: ['contacts'],
  components: {
    ContactDetails,
  },
  methods: {
    deleteContact(contact) {
      this.$emit('deleteContact', contact);
    },
    saveEdit(editedContact) {
      this.$emit('saveEdit', editedContact);
    },
  },
};
</script>
<style scoped>
li {
  list-style: none;
}
</style>
