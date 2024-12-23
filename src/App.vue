<template>
  <div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Contact Manager</h1>
    <ContactFilter @filterContacts="filterContacts" />
    <ContactGrid
      :contacts="filteredContacts"
      @updateContact="updateContact"
      @deleteContact="deleteContact"
      @addContact="addContact"
    />
  </div>
</template>

<script>
import ContactGrid from './components/ContactGrid.vue'
import ContactFilter from './components/ContactFilter.vue'

export default {
  components: {
    ContactGrid,
    ContactFilter,
  },
  data() {
    return {
      contacts: [
        {
          id: 1,
          name: "Alice Johnson",
          email: "alice.johnson@example.com",
          address: "123 Maple Street",
          phone: "123-456-7890",
          country: "USA",
          city: "New York"
        },
        {
          id: 2,
          name: "Bob Smith",
          email: "bob.smith@example.com",
          address: "456 Oak Avenue",
          phone: "987-654-3210",
          country: "Canada",
          city: "Toronto"
        },
        {
          id: 3,
          name: "Carol White",
          email: "carol.white@example.com",
          address: "789 Pine Road",
          phone: "555-123-4567",
          country: "UK",
          city: "London"
        },
        {
          id: 4,
          name: "David Brown",
          email: "david.brown@example.com", address: "321 Elm Street",
          phone: "444-555-6666",
          country: "Australia",
          city: "Sydney"
        },
        {
          id: 5,
          name: "Emily Davis",
          email: "emily.davis@example.com", address: "654 Spruce Lane",
          phone: "333-444-5555",
          country: "USA",
          city: "Los Angeles"
        }
      ],
      filteredContacts: [],
    }
  },
  methods: {
    filterContacts(query) {
      this.filteredContacts = this.contacts.filter(
        (contact) =>
          contact.name.toLowerCase().includes(query.name.toLowerCase()) &&
          contact.email.toLowerCase().includes(query.email.toLowerCase()),
      )
    },
    addContact(newContact) {
      newContact.id = Date.now()
      this.contacts.push(newContact)
      this.filteredContacts = [...this.contacts]
    },
    updateContact(updatedContact) {
      const index = this.contacts.findIndex((c) => c.id === updatedContact.id)
      if (index !== -1) {
        this.contacts[index] = { ...updatedContact }
        this.filteredContacts = [...this.contacts]
      }
    },
    deleteContact(id) {
      this.contacts = this.contacts.filter((contact) => contact.id !== id)
      this.filteredContacts = [...this.contacts]
    },
  },
  created() {
    this.filteredContacts = [...this.contacts]
  },
}
</script>
