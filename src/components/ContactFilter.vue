<template>
  <div class="mb-4 flex space-x-4">
    <input
      v-model="name"
      placeholder="Filter by name"
      class="border border-gray-300 px-4 py-2 rounded w-1/2"
    />
    <input
      v-model="email"
      placeholder="Filter by email"
      class="border border-gray-300 px-4 py-2 rounded w-1/2"
    />
    <button @click="applyFilter" class="bg-blue-500 text-white px-4 py-2 rounded">Filter</button>
  </div>
</template>

<script>
export default {
  data() {
    return { name: '', email: '' }
  },
  methods: {
    applyFilter() {
      this.$emit('filterContacts', { name: this.name, email: this.email })
    },
  },
}
</script>
