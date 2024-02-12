<template>
    <div class="body">

        <img class="logo" src="../components/lOGO UX BUZ PNG 3.png" alt="Ícone" />
        <p class="UX">UXBUS</p>
        
        <p class="vantagens">Tenha todas as vantagens em suas mãos</p>
        <div class="divParagrafoCinza">
            <p>Recarregue seu cartão totalmente online</p>
            <p>Acompanhe a localização em tempo real do seu ônibus</p>
            <p>Visualize as linhas e horários quando e onde quiser</p>
            <p>E muito mais!</p>
        </div>

        <p class="vantagens">Baixe o nosso aplicativo</p>
        <a href="https://play.google.com/store/apps/UXBUS">

          <img class="download" src="../views/image116.png" target="blank" alt="Ícone" />
        </a>
    </div>
  </template>
  
  
  
  <script>
  
  import { BButton } from 'bootstrap-vue'
  
  
  
  export default {
    name: 'Aviso',
    data() {
    return {
      showModal:false,
    };
  },
    components: {
      BButton,
    },
  
  
    mounted() {
   
    },
  
    computed: {
  
    },
  
    watch:{
  
    },
  
    methods: {

    },
  
  }
  </script>
  
  <style scoped>
.download{
  width: 160px;
}
.divParagrafoCinza{
    font-size: 14px;
    color: rgba(250, 250, 250, 0.466);
    width: 220px;
}

  .vantagens{
    color: white;
    font-size: 14px;
    margin-top: 8px;
  }
  .UX{
    color: white;
  }
.logo{
    margin-top: -2rem;

}

  .body{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 101vh;
    min-width: 100vw;
    background-color: #052144;
    margin-top: -3.8rem;
  }
  
 
  </style>
  