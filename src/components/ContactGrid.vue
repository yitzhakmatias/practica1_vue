<template>
  <div class="overflow-auto">
    <table class="table-auto w-full border-collapse border border-gray-200 rounded-md shadow-sm">
      <thead class="bg-gray-50">
        <tr>
          <th class="border border-gray-200 px-4 py-2 text-left">Name</th>
          <th class="border border-gray-200 px-4 py-2 text-left">Email</th>
          <th class="border border-gray-200 px-4 py-2 text-left">Address</th>
          <th class="border border-gray-200 px-4 py-2 text-left">Phone</th>
          <th class="border border-gray-200 px-4 py-2 text-left">Country</th>
          <th class="border border-gray-200 px-4 py-2 text-left">City</th>
          <th class="border border-gray-200 px-4 py-2 text-center">Actions</th>
        </tr>
      </thead>
      <tbody>
        <!-- Existing contacts -->
        <tr
          v-for="(contact, index) in contacts"
          :key="contact.id"
          class="odd:bg-white even:bg-gray-50"
        >
          <td class="border border-gray-200 px-4 py-2 max-w-[150px] truncate">
            <input v-model="contact.name" class="w-full border border-gray-300 rounded px-2 py-1" />
          </td>
          <td class="border border-gray-200 px-4 py-2 max-w-[250px] truncate">
            <input
              v-model="contact.email"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2 max-w-[200px] truncate">
            <input
              v-model="contact.address"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2">
            <input
              v-model="contact.phone"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2">
            <input
              v-model="contact.country"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2">
            <input v-model="contact.city" class="w-full border border-gray-300 rounded px-2 py-1" />
          </td>
          <td class="border border-gray-200 px-4 py-2 text-center space-x-2">
            <button
              @click="saveContact(index)"
              class="bg-blue-500 text-white px-3 py-1 rounded hover:bg-blue-600"
            >
              Save
            </button>
            <button
              @click="deleteContact(contact.id)"
              class="bg-red-500 text-white px-3 py-1 rounded hover:bg-red-600"
            >
              Delete
            </button>
          </td>
        </tr>

        <!-- Row for adding a new contact -->
        <tr class="bg-gray-100">
          <td class="border border-gray-200 px-4 py-2">
            <input
              v-model="newContact.name"
              placeholder="Name"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2">
            <input
              v-model="newContact.email"
              placeholder="Email"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2">
            <input
              v-model="newContact.address"
              placeholder="Address"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2">
            <input
              v-model="newContact.phone"
              placeholder="Phone"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2">
            <input
              v-model="newContact.country"
              placeholder="Country"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2">
            <input
              v-model="newContact.city"
              placeholder="City"
              class="w-full border border-gray-300 rounded px-2 py-1"
            />
          </td>
          <td class="border border-gray-200 px-4 py-2 text-center">
            <button
              @click="addNewContact"
              class="bg-green-500 text-white px-3 py-1 rounded hover:bg-green-600"
            >
              Add
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    contacts: Array,
  },
  data() {
    return {
      newContact: {
        name: '',
        email: '',
        address: '',
        phone: '',
        country: '',
        city: '',
      },
    }
  },
  methods: {
    saveContact(index) {
      this.$emit('updateContact', this.contacts[index])
    },
    deleteContact(id) {
      this.$emit('deleteContact', id)
    },
    addNewContact() {
      if (this.newContact.name && this.newContact.email) {
        this.$emit('addContact', { ...this.newContact })
        this.newContact = {
          name: '',
          email: '',
          address: '',
          phone: '',
          country: '',
          city: '',
        }
      }
    },
  },
}
</script>
