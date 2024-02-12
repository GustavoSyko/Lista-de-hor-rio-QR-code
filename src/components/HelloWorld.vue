<template>
  <div v-if="!showModal" class="testeDiv">
    
    <img src="../components/lOGO UX BUZ PNG 3.png" alt="Ícone" />
    <!-- podemos colocar um loading usando o busy-state -->
    
    <div class="divLabel">
      <h6 class="labelTable">Linhas que passam neste ponto</h6>
    </div>
    
    <b-table class="tableLinhasPonto" :items="tableData" :fields="tableFields" :small="true" @row-clicked="clicouNaLinha">


      <template #cell(iconeBadge)="data">
        <div class="celulaIcone">
          <img class="icone" src="../components/bus-alt.png" width="20px" height="20px" alt="Ícone" />
          <b-badge class="badgeVerde" variant="success">{{ data.item.id }}</b-badge>
        </div>
      </template>
      <template #cell(name)="data">
        <p class="nomeLinhaTabela">{{ data.item.name }}</p>
      </template>

    </b-table>





    <div class="divLabelPonto">
      <h6 class="labelTable2">Linhas / Horários</h6>
    </div>
    <b-table 
      class="tableLinhasPonto" 
      :items="outrasLinhas" 
      :fields="tableFields" 
      :small="true"
      @row-clicked="clicouLinhas"
      >

      <template #cell(iconeBadge)="data">

        <div class="celulaIcone">
          <img class="icone" src="../components/bus-alt.png" width="20px" height="20px" alt="Ícone" />
          <b-badge class="badge" variant="warning">{{ data.item.id }}</b-badge>
          
        </div>
      </template>
      <template #cell(name)="data">
        <div class="nomeLinha">

          <p class="nomeLinhaTabela">{{ data.item.name }}</p>
        </div>
      </template>

    </b-table>
    
    <transition name="slide">
      <b-modal v-model="showModal" id="my-modal">
        <!-- conteúdo do modal -->
      </b-modal>
    </transition>
    
    
  </div>
  
  <transition v-else name="slide-up">
    
    <div >
        <div class="body">
        <img class="logo" src="../components/lOGO UX BUZ PNG 3.png" alt="Ícone" />
        <p class="UX">UXBUS</p>
  
        <p class="vantagens">Tenha todas as vantagens em suas mãos</p>
        <div class="divParagrafoCinza" @click="clicou">
          <p>Recarregue seu cartão totalmente online</p>
          <p>Acompanhe a localização em tempo real do seu ônibus</p>
          <p>Visualize as linhas e horários quando e onde quiser</p>
          <p>E muito mais!</p>
        </div>
  
        <p class="vantagens">Baixe o nosso aplicativo</p>
        
  
          <img class="download" src="../views/image116.png" target="blank" alt="Ícone" />
        
      </div>
    </div>
    
  </transition>
</template>

<script>

import { BTable, BModal } from 'bootstrap-vue'

// verificar outro componente bootstrap para fazer as linhas ( group item talvez algo assims)


export default {
  name: 'Horários',

  data() {
    return {
      showModal: false,
      tableFields: [
        { key: 'iconeBadge', label: '' },
        { key: 'name', label: '' },
        // Mais campos aqui...
      ],
      tableData: [
        { id: 31, name: 'Troncal - Via Rua dos Caçadores', iconeBadge: '' },
        { id: 32, name: 'Troncal - Via Água Verde', iconeBadge: '' },

        // Mais dados aqui...
      ],
      outrasLinhas: [
        { id: 10, name: 'Troncal - Via Rua São Paulo', iconeBadge: '' },
        { id: 11, name: 'Troncal - Via Rua 2 de Setembro', iconeBadge: '' },
        { id: 12, name: 'Troncal - Via Escola Agrícula', iconeBadge: '' },
        { id: 15, name: 'Troncal - Via Ponte Tamarindo', iconeBadge: '' },
        { id: 17, name: 'Troncal - Via Rua das Missões', iconeBadge: '' },
        { id: 30, name: 'Troncal - Via Rua Governador Jorge Lacerda', iconeBadge: '' },
        { id: 31, name: 'Troncal - Via Rua dos Caçadores', iconeBadge: '' },
        { id: 32, name: 'Troncal - Via Água Verde', iconeBadge: '' },
        { id: 70, name: 'Troncal - Via Proeb/Aterro', iconeBadge: '' },
        { id: 80, name: 'Troncal - Via Pedro Zimmermann', iconeBadge: '' },
        { id: 81, name: 'Troncal - Via Gustavo Zimmermann', iconeBadge: '' },
        { id: 109, name: 'Erich Belz', iconeBadge: '' },
        { id: 111, name: 'Santa Clara', iconeBadge: '' },
        { id: 120, name: 'Jardim Germânico', iconeBadge: '' },
        { id: 121, name: 'Distrito Industrial', iconeBadge: '' },
        { id: 122, name: 'Via Moínho', iconeBadge: '' },
        { id: 123, name: 'Itoupavazinha', iconeBadge: '' },
        { id: 124, name: 'Felipe Bauer', iconeBadge: '' },
        { id: 125, name: 'Franz Volles', iconeBadge: '' }
      ],
    };
  },
  mounted() {
    // this.showModal = true;
    setTimeout(() => {
      this.showModal = true
    },100)
    setTimeout(() => {
      this.showModal = false
    }, 5500)
  },

  components: {
    BTable,
    BModal,

  },
  methods: {

    clicou(){
      this.showModal = false
    },  
    
    clicouLinhas(){
      this.showModal = true
      setTimeout(() => {
      this.showModal = false
    }, 4500)
    },

    clicouNaLinha(item, index, event) {
      this.$router.push({ name: 'about', params: { id: item.id } })
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

template{
  
}

.slide-up-enter-active {
  transition: all 3s;
}
.slide-up-leave-active {
  transition: all 2s;
}
.slide-up-enter, .slide-up-leave-to {
  transform: translateY(100%);
}
.slide-up-leave, .slide-up-enter-to {
  transform: translateY(0);
}
.download {
  width: 160px;
  max-width: 526px;
}

.divParagrafoCinza {
  font-size: 14px;
  color: rgba(250, 250, 250, 0.466);
  width: 220px;
  max-width: 526px;
}

.vantagens {
  color: white;
  font-size: 14px;
  margin-top: 8px;
  max-width: 526px;
}

.UX {
  color: white;
  max-width: 526px;
}

.logo {
  margin-top: -2rem;
  max-width: 526px;
}

.body {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 101vh;
  min-width: 100vw;
  background-color: #052144;
  margin-top: -3.8rem;
  max-width: 526px;
}

.slide-enter,
.slide-leave-to {
  transform: translateY(100%);
}

.icone {
  color: #9c9c9c;
  max-width: 526px;
}

.badge {
  font-size: 12px;
  max-width: 526px;
}

.badgeVerde {
  font-size: 12px;
  background-color: #0E7632;
  max-width: 526px;
}

.logo {
  margin-bottom: 30px;
  max-width: 526px;
}

.divLabel {
  width: 100%;
  margin-top: 1.4rem;
  max-width: 526px;
}

.divLabelPonto {
  width: 88%;
  border-top: solid 1px rgba(0, 0, 0, 0.121);
  padding-top: 1rem;
  max-width: 526px;
}

.labelTable {
  display: flex;
  width: auto;
  margin-left: 1.4rem;
  font-size: 15px;
  font-weight: bold;
  color: #0021a3;
  max-width: 526px;
}

.labelTable2 {
  display: flex;
  width: auto;
  font-size: 15px;
  font-weight: bold;
  color: #0021a3;
  max-width: 526px;
}

.nomeLinha {
  max-width: 526px;
}

.nomeLinhaTabela {
  font-size: 3vw;
  height: 10px;
  min-width: 220px;
  margin-top: 8px;

  @media screen and (max-width: 426px) {
    font-size: 11px;
    font-weight: 400;
  }

  max-width: 526px;
}

.tableLinhasPonto {
  font-size: 12px;
  margin-bottom: -0.2rem;
  width: 88%;
  max-width: 526px;
}

.celulaIcone {
  margin-left: -5px;
  display: flex;
  margin-top: 6px;
  gap: 4px;
  max-width: 526px;
}

.testeDiv {
  margin-top: -30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 526px;
}


@media screen and (min-width: 527px) {

  .download,
  .divParagrafoCinza,
  .vantagens,
  .UX,
  .logo,
  .body,
  .slide-enter,
  .icone,
  .badge,
  .badgeVerde,
  .divLabel,
  .divLabelPonto,
  .labelTable,
  .labelTable2,
  .nomeLinha,
  .nomeLinhaTabela,
  .tableLinhasPonto,
  .celulaIcone,
  .testeDiv {
    display: none;
  }
}

</style>
