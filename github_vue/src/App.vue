<template>
  <div id="app">
    <Navbar/>

    <div class="container">
      <div class="card card-body">
        <h1>Pesquisar Usuarios do GitHub</h1>
        <p class="lead">Digite um nome para encontrar usuários e repositórios</p>
        <input @keyup="getUser" id="search" type="text" class="form-control" required>
      </div>
    </div>
  </div>
</template>

<script>

import Navbar from "./components/Navbar.vue";
import axios from 'axios';

export default {
  name: "app",
  data() {
    return {
      github: {
        url: 'https://api.github.com/users',
        client_id: 'e53febbd554644d70b00',
        client_secret: '0eabb5d3af6d3ae419c42913f660f0523a19140e',
        count: 7,
        sort: 'created: asc'
      },
      user: [],
      repos: []
    }
  },
  components: {
    Navbar
  },
  methods: {
    getUser(e){
      const user = e.target.value;
      const { url, client_id, client_secret, count, sort } = this.github;
      axios.get(
        `${url}/${user}?client_id=${client_id}&client_secret=${client_secret}`
      )
      .then(({ data }) => console.log(data))
    }
  }
};
</script>
