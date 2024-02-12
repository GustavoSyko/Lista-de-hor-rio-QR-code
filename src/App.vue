<template>
  <div id="app">
    <nav class="teste">
      <h1 class="abraNoCelular">Abra no celular, ou coloque em modo Celular</h1>
    <h1 class="abraNoCelular">Aperte CTRL + SHIFT + I</h1>
    <h1 class="abraNoCelular">E selecione na caixa a direita</h1>
      <img class="abraNoCelular" src="../src/components/Captura de tela 2024-02-12 000549.png" width="800px" height="680px" alt="teste">


      <!-- <router-link to="/">Home</router-link>  -->
      <!-- <router-link to="/about">About</router-link> -->
    </nav>
    <router-view/>
  </div>
</template>

<style>

@media screen and (max-width: 526px) {
  .abraNoCelular{
    display: none;
  }
}
@media screen and (min-width: 526px) {
  .abraNoCelular{
    display: block;
  }
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.teste{
  display: flex;
  justify-content: center;
  text-align: center;
  flex-direction: column;
  align-items: center;
}
  
nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
