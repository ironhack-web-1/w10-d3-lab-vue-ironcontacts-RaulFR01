<template>
  <div id="app">
    <h1>IronContacts</h1>
    <button v-on:click="addCharacter()">Add random character</button>
    <table style="border: 1px solid black">
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won Oscar</th>
          <th>Won Emmy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in ListOfContacts" :key="contact.name">
          <td>
            <img
              :src="contact.pictureUrl"
              :alt="`picture of` + contact.name"
              style="width: 150px; height: 200px"
            />
          </td>
          <td>
            <p>{{ contact.name }}</p>
          </td>
          <td>
            <p>{{ contact.popularity.toFixed(2) }}</p>
          </td>
          <td>{{ isTrophy(contact.wonOscar) }}</td>
          <td>{{ isTrophy(contact.wonEmmy) }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import contacts from "./contacts.json";
export default {
  data() {
    return {
      ListOfContacts: []
        
    };
  },
  mounted(){
    this.ListOfContacts = contacts.slice(0,5)
  },
  methods: {
    isTrophy(value) {
      if (value === true) {
        return "🏆";
      }
    },
    addCharacter(){
      const random = Math.floor(Math.random()*contacts.length);
      const character = contacts[random];
      this.ListOfContacts.push(character)
      console.table(this.ListOfContacts);
    }
  },
};
</script>
