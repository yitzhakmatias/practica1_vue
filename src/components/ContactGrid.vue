<template>
  <div class="overflow-x-auto">
    <table class="table-auto w-full border border-gray-300 rounded-lg">
      <thead>
        <tr class="bg-gray-100">
          <th class="px-4 py-2">Name</th>
          <th class="px-4 py-2">Email</th>
          <th class="px-4 py-2">Address</th>
          <th class="px-4 py-2">Phone</th>
          <th class="px-4 py-2">Country</th>
          <th class="px-4 py-2">City</th>
          <th class="px-4 py-2">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(contact, index) in contacts" :key="contact.id" class="hover:bg-gray-50">
          <td class="border px-4 py-2">
            <input v-model="contact.name" class="w-full border border-gray-300 rounded px-2" />
          </td>
          <td class="border px-4 py-2">
            <input v-model="contact.email" class="w-full border border-gray-300 rounded px-2" />
          </td>
          <td class="border px-4 py-2">
            <input v-model="contact.address" class="w-full border border-gray-300 rounded px-2" />
          </td>
          <td class="border px-4 py-2">
            <input v-model="contact.phone" class="w-full border border-gray-300 rounded px-2" />
          </td>
          <td class="border px-4 py-2">
            <input v-model="contact.country" class="w-full border border-gray-300 rounded px-2" />
          </td>
          <td class="border px-4 py-2">
            <input v-model="contact.city" class="w-full border border-gray-300 rounded px-2" />
          </td>
          <td class="border px-4 py-2 text-center">
            <button
              @click="saveContact(index)"
              class="bg-blue-500 text-white px-4 py-1 rounded hover:bg-blue-600 mr-2"
            >
              Save
            </button>
            <button
              @click="deleteContact(contact.id)"
              class="bg-red-500 text-white px-4 py-1 rounded hover:bg-red-600"
            >
              Delete
            </button>
          </td>
        </tr>
        <tr>
          <td class="border px-4 py-2">
            <input
              v-model="newContact.name"
              placeholder="Name"
              class="w-full border border-gray-300 rounded px-2"
            />
          </td>
          <td class="border px-4 py-2">
            <input
              v-model="newContact.email"
              placeholder="Email"
              class="w-full border border-gray-300 rounded px-2"
            />
          </td>
          <td class="border px-4 py-2">
            <input
              v-model="newContact.address"
              placeholder="Address"
              class="w-full border border-gray-300 rounded px-2"
            />
          </td>
          <td class="border px-4 py-2">
            <input
              v-model="newContact.phone"
              placeholder="Phone"
              class="w-full border border-gray-300 rounded px-2"
            />
          </td>
          <td class="border px-4 py-2">
            <input
              v-model="newContact.country"
              placeholder="Country"
              class="w-full border border-gray-300 rounded px-2"
            />
          </td>
          <td class="border px-4 py-2">
            <input
              v-model="newContact.city"
              placeholder="City"
              class="w-full border border-gray-300 rounded px-2"
            />
          </td>
          <td class="border px-4 py-2 text-center">
            <button
              @click="addNewContact"
              class="bg-green-500 text-white px-4 py-1 rounded hover:bg-green-600"
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
      if (
        this.newContact.name &&
        this.newContact.email &&
        this.newContact.address &&
        this.newContact.phone &&
        this.newContact.country &&
        this.newContact.city
      ) {
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
