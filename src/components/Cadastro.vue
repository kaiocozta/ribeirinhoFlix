<template>

  <div id="cadastro">

    <div class="cabecalho">

      <img class="logo" src="../img/logo.jpg">

      <a id="logar" href="/"><b>Entrar</b></a>

    </div>

    <div class="formulario-cadastro">
      <br>
      <h2>Crie sua conta &nbsp &nbsp &nbsp &nbsp &nbsp &nbsp</h2>
      <form @submit="cadastrar">

        <input id="userEmail" type="email" placeholder="Informe um email" width="100px" v-model="novoUser.email"
               required><br></br>

        <input id="userSenha" type="password" placeholder="Digite uma senha" v-model="novoUser.senha" required>

        <br><br><br><br>
        <button class="cell" type="submit"><b>Criar conta</b></button>
      </form>
    </div>

  </div>

</template>

<script>
  export default {
    name: "Cadastro",
    data() {
      return {
        users: [{
          email: '',
          senha: ''
        }],
        novoUser: {
          email: '',
          senha: ''
        },
        userExistente: false,
        userSalvo: null
      }
    },
    created() {
      this.$http.get('http://localhost:3000/users').then(response => {
        this.users = response.body;
      });
    },
    methods: {
      login() {
        this.$router.push('/');
      },
      cadastrar(e) {
        e.preventDefault();

        for (var user in this.users) {
          if (document.getElementById("userEmail").value === this.users[user].email) {
            this.userExistente = true;
          }
        }
        if (!this.userExistente) {
          this.$http.post('http://localhost:3000/users', {
            email: this.novoUser.email,
            senha: this.novoUser.senha
          }).then(response => {
            this.userSalvo = response.body;
            alert("Usuário cadastrado");
            this.login();
          });

        } else {
          alert("Usuário já existe");
          this.reload();
        }

      },
      reload: function () {
        this.$router.go(this.$router.currentRoute);
      }
    }
  }
</script>

<style scoped>

  .cell {
    cursor: cell;
  }

  .logo {
    width: 180px;
    height: 50px;
    margin: 20px;
  }

  .formulario-cadastro {
    width: 300px;
    height: 450px;
    margin: auto;
    border-radius: 4px;
    text-align: center;
  }

  button {
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

  #logar {
    color: #0e0f11;
    float: right;
    margin: 30px;
  }

</style>
