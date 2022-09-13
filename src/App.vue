<template>
  <div id="app">
    <h1>IronContacts</h1>
    <button v-on:click="addCharacter()">Add random character</button>
    <button v-on:click="sortByPopularity()">Sort by popularity</button>
    <button v-on:click="sortByName()">Sort by name</button>
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
      let randomNumber = Math.floor(Math.random()*contacts.length);
      let character = contacts[randomNumber];
      console.log(character.name)
      if(!this.ListOfContacts.includes(character)){
        this.ListOfContacts.push(character)
      }
    },
    sortByPopularity(){
      this.ListOfContacts.sort((a,b) => b.popularity - a.popularity);
    },
    sortByName(){
      this.ListOfContacts.sort((a,b) => a.name.localeCompare(b.name));
      console.table(this.ListOfContacts);
    }
  },
};
</script>
