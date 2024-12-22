<template>
  <div>
    <input v-model="name" placeholder="Filter by name" />
    <input v-model="email" placeholder="Filter by email" />
    <button @click="applyFilter">Filter</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      email: '',
    };
  },
  methods: {
    applyFilter() {
      this.$emit('filterContacts', { name: this.name, email: this.email });
    },
  },
};
</script>
