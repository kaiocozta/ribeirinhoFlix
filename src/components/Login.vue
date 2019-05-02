<template>

  <div id="login">

    <div class="contain-imagem">

      <img class="logo" src="../img/logo.jpg">

    </div>

    <div class="entrar">
      <br>

      <h1>Entrar &nbsp &nbsp &nbsp &nbsp &nbsp &nbsp &nbsp &nbsp</h1>
      <form @submit="logar">
        <input id="userEmail" type="email" placeholder="Digite seu email" width="100px">
        <br><br>
        <input id="userSenha" type="password" placeholder="Digite sua senha">
        <br><br>
        <button type="submit"><b>Entrar</b></button>
      </form>
      <h4>Não possui uma conta?</h4>
      <button type="button" v-on:click="cadastro"><b>Cadastre-se</b></button>

    </div>
  </div>
</template>

<script>
  var user;
  export default {
    name: "login",
    data() {
      return {
        users: [],
        usuarioExistente: false
      }
    },
    created() {
      this.$http.get('http://localhost:3000/users').then(response => {
        this.users = response.body;
      });
    },
    mounted() {
      console.log(document.getElementsByName('div'));
      //document.getElementsByName('body').css('background-color','black');
    },
    methods: {
      cadastro() {
        this.$router.push('/cadastro');
      },
      logar() {
        for (var user in this.users) {
          if (document.getElementById("userEmail").value === this.users[user].email &&
            document.getElementById("userSenha").value === this.users[user].senha) {
            this.$router.push('/filmes');
            this.usuarioExistente = true;
          }
        }
        if (!this.usuarioExistente) {
          alert("Email ou senha inválido");
        }
        this.reload();
      },
      reload: function () {
        this.$router.go(this.$router.currentRoute);
      }
    }
  }
</script>

<style scoped>

  h1 {
    color: #0e0f11;
  }

  .entrar {
    width: 300px;
    height: 450px;
    margin: auto;
    background-color: rgba(0, 0, 0, .75);
    border-radius: 4px;
    text-align: center;
  }

  .logo {
    width: 180px;
    height: 50px;
    margin: 20px;
  }

  h1, h4 {
    color: white;
  }

  button {
    cursor: pointer;
    width: 220px;
    height: 26px;
    border-radius: 2px;
    color: white;
    border: 0;
    background-color: #ff0025;
  }

  input {
    border-radius: 5px;
    width: 220px;
    height: 23px;
  }

</style>
