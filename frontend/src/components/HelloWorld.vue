<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>

    <table class="table">
        <thead class="thead-dark">
          <tr>
            <th scope="col">#</th>
            <th scope="col">username</th>
            <th scope="col">email</th>
            <th scope="col">url</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in users">
            <th scope="row">1</th>
            <td>{{ item.username }}</td>
            <td>{{ item.email }}</td>
            <td>{{ item.url }}</td>
          </tr>
        </tbody>

    </table>
    <div>resultados: {{ cantidad }}</div>
    <button type="button" v-on:click="featchAPIData()">Fetch</button>

    <br />
    <div id="example-1">
      <button v-on:click="counter += 1">Add 1</button>
      <p>Se ha hecho clic en el botón de arriba {{ counter }} veces.</p>
    </div>


    <ul>
      <li>
        <a
          href="https://vuejs.org"
          target="_blank"
        >
          Core Docs
        </a>
      </li>
      <li>
        <a
          href="https://forum.vuejs.org"
          target="_blank"
        >
          Forum
        </a>
      </li>
      <li>
        <a
          href="https://chat.vuejs.org"
          target="_blank"
        >
          Community Chat
        </a>
      </li>
      <li>
        <a
          href="https://twitter.com/vuejs"
          target="_blank"
        >
          Twitter
        </a>
      </li>
      <br>
      <li>
        <a
          href="http://vuejs-templates.github.io/webpack/"
          target="_blank"
        >
          Docs for This Template
        </a>
      </li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li>
        <a
          href="http://router.vuejs.org/"
          target="_blank"
        >
          vue-router
        </a>
      </li>
      <li>
        <a
          href="http://vuex.vuejs.org/"
          target="_blank"
        >
          vuex
        </a>
      </li>
      <li>
        <a
          href="http://vue-loader.vuejs.org/"
          target="_blank"
        >
          vue-loader
        </a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/awesome-vue"
          target="_blank"
        >
          awesome-vue
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      counter: 0,
      cantidad: 0,
      users: [],
    }
  },
  methods: {
      featchAPIData() {
        this.responseAvailable = false;
        fetch("http://localhost:8000/users/", {
            "method": "GET",
            "headers": {
            }
        })
        .then(response => { 
            //alert("first response");
            if(response.ok){
                return response.json()    
            } else {
                alert("Server returned " + response.status + " : " + response.statusText);
            }                
        })
        .then(response => {
            this.users = response.results; 
            this.cantidad = response.count; 
            this.responseAvailable = true;
        })
        .catch(err => {
            console.log(err);
        });
      },
      save: function() {
            this.$http.post(this.endpoint, {
                "username": this.username,
                "email": this.email,
                "url": this.url,
            }).then(function(response){
            console.log('Respuesta del servidor: ' + response);
            this.users = response.body;
          }, function(){
            alert('Error on save!')
          })
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
