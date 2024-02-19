<template>
  <div class="divFundo"> 
    <img  class="abraNoCelular" src="../../public/—Pngtree—smartphone mockup blank display android_6073224.png" width="340px" height="680px" alt="teste"> 
  <div v-if="!showModal && !mostrarViewHorarios" class="testeDiv">
    
    <div class="divTables">

    
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
        <div class="celulaIcone">
          <p class="nomeLinhaTabela">{{ data.item.name }}</p>

        </div>
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
          <b-badge class="badgeAmarela" variant="warning">{{ data.item.id }}</b-badge>
          
        </div>
      </template>
      <template #cell(name)="data">
        <div class="celulaIcone">

          <p class="nomeLinhaTabela">{{ data.item.name }}</p>
        </div>
      </template>

    </b-table>
  </div>
    <!-- <transition name="slide">
      <b-modal v-model="showModal" id="my-modal">
        conteúdo do modal
      </b-modal>
    </transition> -->
    
    
  </div>
  
  <transition  name="slide-up">
    
    <div  v-if="showModal">
      <!-- <img class="abraNoCelular" src="../../public/—Pngtree—smartphone mockup blank display android_6073224.png" width="360px" height="740px" alt="teste">  -->
        <div class="body">
          <div class="divInformacoes">
            
            <img class="logo" src="../components/lOGO UX BUZ PNG 3.png" alt="Ícone" />
            <p class="UX">UXBUS</p>
      
            <p class="vantagens">Tenha todas as vantagens em suas mãos</p>
            <div class="divParagrafoCinza">
              <p>Faça a recarga totalmente online</p>
              <p>Acompanhe o ônibus em tempo real</p>
              <p>Visualize todas as linhas</p>
              <!-- <p>E muito mais!</p> -->
            </div>
      
            <p class="vantagens">Baixe o nosso aplicativo</p>
            <a href="https://play.google.com/store/search?q=uxbus&c=apps">
              <img class="download" src="../views/image116.png" target="blank" alt="Ícone" />
            </a>
          </div>

          <transition name="fade">
            <div class="labelOu"  v-if="showText">
              <p >Ou</p>
              <b-button @click="clicou" class="botaoVersaoLimitada" variant="success">Continuar com a versão limitada</b-button>
            </div>
          </transition>

      </div>
    </div>
    
  </transition>


  <div class="about" v-if="mostrarViewHorarios && !showModal">
    
    <div class="nav">
      <b-button 
        class="botaoVoltar" 
        @click="voltar"
        >
        <img src="../views/Frame 805.png" alt="Ícone" />
      </b-button>
    </div>
    <img src="../views/lOGO UX BUZ PNG 3.png" alt="Ícone" />

    <div class="divNumeroLinha">
      <div class="divBadgeIcon">
        <b-badge class="badgeId shadow">{{ id }}</b-badge>
        <img src="../views/Vector.png" width="24px" height="24px" alt="Ícone" />
        <p class="nomeLinha">{{ linha }}</p>
      </div>
    </div>

    <div class="divSentidoTrajeto" v-if="this.linhaSelecionada.horarios">

      <p class="saidaTrajeto">{{ this.ida ? this.linhaSelecionada.horarios.ida.trajeto.saida :  this.linhaSelecionada.horarios.volta.trajeto.saida}}</p>
      <img class="flechaAzul" src="../views/flechaazulAtual.png" width="24px" height="28px" alt="Ícone" />
      <p class="saidaTrajeto">{{ this.ida ? this.linhaSelecionada.horarios.ida.trajeto.chegada :  this.linhaSelecionada.horarios.volta.trajeto.chegada}}</p>
      
      <b-button 
      class="flechas"
      @click="trocarSentidoRota"
      > 
        <img  src="../components/Union.png" width="20px" height="20px" alt="Ícone" />
      </b-button>
    </div>

    <div  v-if="this.linhaSelecionada.horarios">
      <div class="divColuna" v-for="horas in horarios">

        <div class="divHorarios">
          <div class="divIconeHora">
            <p class="hora">{{ horas }}</p>
            <img class="cadeiraRoda" src="../views/Cadeira de roda.png" width="16px" height="14px" alt="Ícone" />
          </div>

          <p class="labelTrajeto">{{ labelLinha }}</p>

        </div>
      </div>
    </div>

  </div>
</div>
</template>

<script>

import { BTable, BModal, BBadge, BButton } from 'bootstrap-vue'
import {FadeTransition} from 'vue2-transitions'

// verificar outro componente bootstrap para fazer as linhas ( group item talvez algo assims)


export default {
  name: 'Horários',

  data() {
    return {
      isPrimeiravez: false,
      showModal: false,
      showText: false,
      mostrarViewHorarios: false,
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
        { id: 125, name: 'Franz Volles', iconeBadge: '' },
      ],
      id: '',
      linha: '',
      horarios: [],
      labelLinha:'',
      ida: true,
      linhas: [
        { id: 31, name: 'Troncal - Via Rua dos Caçadores', iconeBadge: '' },
        { id: 32, name: 'Troncal - Via Água Verde', iconeBadge: '' },
      ],
      linhaSelecionada: {},
      rotas: [{
        
          id: 31,
          horarios: {
            ida: {
              trajeto: {
                label: 'Terminal Velha/ Via rua dos caçadores',
                saida: 'Term Garcia',
                chegada: 'Term Velha'
              },
              horarios: ["00:10", "03:58", "04:30", "05:00", "05:30", "06:00", "06:20",
                "06:46", "07:00", "08:25", "08:45", "09:25", "10:00", "10:35", "10:55",
                "11:15", "11:40", "12:00", "12:22", "12:55", "13:14", "13:50", "14:14",
                "14:40", "15:00", "15:30", "16:00", "16:30", "17:00", "17:30", "18:00",
                "18:30", "19:00", "19:30", "20:00", "20:30", "21:00", "21:30", "22:00",
                "22:30", "23:00", "23:30"]
            },
            volta: {
              trajeto: {
                label: 'Terminal Garcia/ Via rua dos caçadores',
                saida: 'Term Velha',
                chegada: 'Term Garcia'
              },
              horarios: ["00:15", "04:05", "04:45", "05:15", "05:45", "06:15", "06:35",
                "07:01", "07:15", "08:40", "09:00", "09:40", "10:15", "10:50", "11:10",
                "11:30", "11:55", "12:15", "12:37", "13:10", "13:29", "14:05", "14:29",
                "14:55", "15:15", "15:45", "16:15", "16:45", "17:15", "17:45", "18:15",
                "18:45", "19:15", "19:45", "20:15", "20:45", "21:15", "21:45", "22:15",
                "22:45", "23:15", "23:45"]
            },
          }
        
      },

      {
        
          id: 32,
          horarios: {
            ida: {
              trajeto: {
                label: 'Terminal Velha/Proeb/Fonte Via Ág. Verde',
                saida: 'Term Velha',
                chegada: 'Term Fonte'
              },
              horarios: ["00:20", "04:10", "04:50", "05:20", "05:50", "06:25", "06:50", "07:10",
                "07:30", "08:55", "09:15", "09:55", "10:30", "11:05", "11:25", "11:45", "12:10",
                "12:30", "12:52", "13:25", "13:44", "14:20", "14:44", "15:10", "15:30", "16:00",
                "16:30", "17:00", "17:30", "18:00", "18:30", "19:00", "19:30", "20:00", "20:30",
                "21:00", "21:30", "22:00", "22:30", "23:00", "23:30"]
            },
            volta: {
              trajeto: {
                label: 'Terminal Fonte/Proeb/Velha Via Ág. Verde',
                saida: 'Term Fonte',
                chegada: 'Term Velha'
              },
              horarios: ["00:25", "04:15", "04:55", "05:25", "05:55", "06:30", "06:55", "07:20",
                "07:40", "09:05", "09:30", "10:05", "10:45", "11:15", "11:35", "11:55", "12:20",
                "12:45", "13:02", "13:35", "13:59", "14:35", "14:59", "15:25", "15:50", "16:20",
                "16:50", "17:20", "17:50", "18:20", "18:50", "19:20", "19:50", "20:20", "20:50",
                "21:20", "21:50", "22:20", "22:50", "23:20", "23:50"]
            },
          }
        
      }]
    };
  },
  mounted() {
   this.showModal = true;
  //  setTimeout(() => {
  //    this.showModal = true
  //  },100)
   setTimeout(() => {
     this.showModal = false
     this.showText = false
   }, 8000000)
  
  setTimeout(() => {
      this.showText = true
    }, 2500)
  },

  components: {
    BTable,
    BModal,
    BBadge,
    BButton,
    FadeTransition,

  },
  watch:{
    ida: function(novoValor, valorAntigo){
      if (this.ida) {
        this.horarios = this.linhaSelecionada.horarios.ida.horarios
        this.labelLinha = this.linhaSelecionada.horarios.ida.trajeto.label
      }else{
        this.horarios = this.linhaSelecionada.horarios.volta.horarios
        this.labelLinha = this.linhaSelecionada.horarios.volta.trajeto.label
      }
      console.log(this.horarios)
    },
    
  },
  methods: {

    trocarSentidoRota(){
      return this.ida = !this.ida
    },

    clicou(){
      this.showModal = false
      this.showText = false
    },  
    
    clicouLinhas(){
      this.showModal = true
      setTimeout(() => {
     this.showModal = false
     this.showText = false
   }, 8000)
      setTimeout(() => {
      this.showText = true
    }, 2500)
    },

    voltar() {
      this.mostrarViewHorarios = false
    },

    clicouNaLinha(item, index) {
      // this.showModal = false
      this.id = item.id
      let linhaFiltrada = this.linhas.filter(linha => linha.id == item.id);
      if (linhaFiltrada.length > 0) {
        this.linha = linhaFiltrada[0].name;
        console.log(this.linha);
      }
      this.linhaSelecionada = this.rotas.find(rota => rota.id == this.id)
      console.log(this.id)
      console.log(this.linhaSelecionada)
      
      if (this.ida) {
        this.horarios = this.linhaSelecionada.horarios.ida.horarios
        this.labelLinha = this.linhaSelecionada.horarios.ida.trajeto.label
      }else{
        this.horarios = this.linhaSelecionada.horarios.volta.horarios
        this.labelLinha = this.linhaSelecionada.horarios.volta.trajeto.label
      }
      this.mostrarViewHorarios = true
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


@media screen and (min-width: 527px) {
  .abraNoCelular{
    background-color: rgba(255, 255, 255, 0);
    z-index: 0;
    position: fixed;
  }
}

.labelOu{
  color: rgba(255, 255, 255, 0.641);
  margin-top: 25px;
  /* margin-bottom: -1.2rem;
  position: fixed;
  bottom: 5rem; */

  /* margin: -8px 0 0 0;  */
}
.botaoVersaoLimitada{
  margin-top:-0.5rem;
  margin-bottom: 1.5rem;
  font-size: 14px;
  position: relative;
  z-index: 1;
  color: rgba(255, 255, 255, 0.834);
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 3s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.fade-leave, .fade-enter-to {
  opacity: 1;
}

.slide-up-enter-active {
  transition: all 1.5s;
}
.slide-up-leave-active {
  transition: all 0s;
}
.slide-up-enter, .slide-up-leave-to {
  transform: translateY(100%);
}
.slide-up-leave, .slide-up-enter-to {
  transform: translateY(0);
}

.divIconeHora{
  display: flex;
  justify-content: center;
  gap: 5px;
  margin-right: 16px;
  /* margin-top: 10px; */
  /* align-items: center; */
}  


.saidaTrajeto{
font-weight: 600;
font-size: 15px;
color: #5A7495;
}
.hora{
  /* margin-right: 1rem; */
  font-size: 0.8rem;
  font-weight: 600;
  color: rgba(0, 0, 0, 0.442);

}

.divHorarios{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 70px;
  flex-direction: row;
}

.divColuna{
  display: flex;
  flex-direction: column;
}



.labelTrajeto{
  font-size: 16px;
  width: 170px;
  line-height: 14px;
  color: rgba(0, 0, 0, 0.54);
}

.flechaAzul{
  margin: -2px 14px 0px 14px;
}
.flechas {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: transparent;
  border-color: transparent;
  position: relative;
  z-index: 1;
  margin-left: 12px;
  width: 24px;
  height: 24px;
}
.flechas:hover {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: transparent;
  border-color: transparent;
  position: relative;
  z-index: 1;
  margin-left: 12px;
  width: 24px;
  height: 24px;
}


.divSentidoTrajeto{
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin-top: 6px;
}
.nav {
  display: flex;
  height: 4px;
  margin-top: -2.5rem;
  @media screen and (min-width: 527px) {
    display: flex;
  height: 4px;
  margin-top: 1.5rem;

  }
}

.botaoVoltar {
  background-color: transparent;
  border-color: transparent;
  position: relative;
  z-index: 1;
  
  /* height: 24px;
  width: 24px; */
  left: 0;
}
.botaoVoltar:hover {
  background-color: transparent;
  border-color: transparent;
  position: relative;
  z-index: 1;
  background-color: transparent;

  /* height: 24px;
  width: 24px; */
  left: 0;
}

.nomeLinha {
  display: flex;
  color: white;
  justify-content: center;
  margin: auto auto auto 8px;
  font-weight: 400;
  letter-spacing: -0.1rem;
  line-height: 1.2rem;
  font-size: 20px;
  margin-left: 16px;

}

.badgeId {
  font-size: 24px;
  border-radius: 12px;
  background-color: #0E7632;
  margin-left: 26px;
  margin-right: 8px;

}

.divBadgeIcon {

  display: flex;
  /* width: auto; */
  flex-direction: row;
  align-items: center;
  justify-content: center;
  align-items: center;
}

.divNumeroLinha {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: start;
  width: auto;
  margin-top: 0.2rem;
  height: 82px;
  background-color: #052144;

  @media screen and (min-width: 527px) {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: start;
    margin-top: 1.5rem;
    width: 100%;
    height: 82px;
    background-color: #052144;

  }
}

.download {
  margin-top: -0.7rem;
  margin-bottom: 1.5rem;
  padding: 0px;
  height: 120px;
  width: 160px;
  max-width: 526px;
  @media screen and (min-width: 527px) {
    position: relative;
    z-index: 1;

  }
}

.divParagrafoCinza {
  font-size: 14px;
  color: rgba(250, 250, 250, 0.51);
  width: 230px;
  max-width: 526px;
  margin-top: 5px;
}

.vantagens {
  color: white;
  font-size: 16px;
  margin-top: 1.4rem;
  margin-bottom: 4px;
  max-width: 526px;
}

.UX {
  color: white;
  max-width: 526px;
  margin-top: -1.5rem;
}

.logo {
  margin-top:   5rem;  
  max-width: 526px;
}

.divInformacoes{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* padding-top: -5rem; */
  height: 420px;
  /* position: fixed; */
  /* top: 0; */
}

.divFundo{
  @media screen and (min-width: 527px) {
    position: fixed;
    top: 0;
    background-color: rgba(0, 0, 0, 0.952);
    display: flex;
    min-height: 100vh;
    min-width: 100vw;
    justify-content: center;
    align-items: center;

  }
}
.body {
  /* display: flex; */
  /* flex-direction: column; */
  /* justify-content: center; */
  /* align-items: center; */
  min-height: 101vh;
  /* height: 101vh; */
  min-width: 100vw;
  background-color: #052144;
  /* margin-top: -1.3rem; */
  max-width: 526px;

  @media screen and (min-width: 527px) {
  min-width: 310px;
  min-height: 660px;
  max-width: 310px;
  max-height: 660px;
  background-color: #052144;
  margin-top: 1.5rem;
  margin-bottom: 1.5rem;
  border-radius: 25px;
  }
}

.slide-enter,
.slide-leave-to {
  transform: translateY(100%);
}

.icone {
  color: #9c9c9c;
}

.badgeAmarela {
  font-size: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 26px;
  height: 24px;
  margin-right: 8px;
  background-color: #DAB500;
  color: rgba(0, 0, 0, 0.565);
}

.badgeVerde {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 26px;
  height: 24px;
  font-size: 12px;
  background-color: #0E7632;
}

.logo {
  margin-bottom: 30px;
}

.divLabel {
  width: 100%;
  margin-top: 1.4rem;
}

.divLabelPonto {
  width: 88%;
  /* border-top: solid 1px rgba(0, 0, 0, 0.121); */
  padding-top: 1rem;
}

.labelTable {
  display: flex;
  width: auto;
  margin-left: 1.4rem;
  font-size: 15px;
  font-weight: bold;
  color: #0021a3;
}

.labelTable2 {
  display: flex;
  width: auto;
  font-size: 15px;
  font-weight: bold;
  color: #0021a3;
}

.nomeLinha {
  /* display: flex; */
  /* align-items: center; */
  /* justify-content: center; */
  /* min-width: fit-content; */

}

.nomeLinhaTabela {
  display: flex;
  text-align: left;
  /* justify-content: start; */
  margin-top: 1rem;
  font-size: 16px;
  
  /* height: 18px; */
  /* min-width: 220px; */
  color: rgba(0, 0, 0, 0.782);

  @media screen and (max-width: 426px) {
    font-size: 14px;
    /* font-weight: 400; */
  }

}

.tableLinhasPonto {
  font-size: 12px;
  margin-bottom: -0.2rem;
  width: 88%;
  @media screen and (min-width: 527px) {
    
  }
}

.celulaIcone {
  margin-left: -5px;
  display: flex;
  justify-content: left;
  align-items: center;
  height: 50px;
  gap: 4px; 
}

.divTables::-webkit-scrollbar {
    width: 0px;
    border-radius: 999px;
}

.divTables::-webkit-scrollbar-track {
    /* background: #f1f1f15f; */
    opacity: 0;
}

.divTables::-webkit-scrollbar-thumb {
    /* background: #dab600ad; */
    /* border-radius: 999px; */
    opacity: 0;
}

.divTables::-webkit-scrollbar-thumb:hover {
    /* background: #977e00; */
    opacity: 0;
}

.divTables{
  @media screen and (min-width: 527px) {
    margin-top: 1.5rem;
    overflow-y: auto;
    /* width: 360px; */
    /* height: 740px;   */
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  z-index: 1;
    
    /* max-width: 360px;
    max-height: 740px;   */
    /* background-color: white; */
    
    /* height: 739px; */
  }
}

.about::-webkit-scrollbar {
    width: 0px;
    border-radius: 999px;
}

.about::-webkit-scrollbar-track {
    /* background: #f1f1f15f; */
    opacity: 0;
}

.about::-webkit-scrollbar-thumb {
    /* background: #dab600ad; */
    /* border-radius: 999px; */
    opacity: 0;
}

.about::-webkit-scrollbar-thumb:hover {
    /* background: #977e00; */
    opacity: 0;
}
.about{
  margin-top: 3.5rem;

  @media screen and (min-width: 527px) {
    overflow-y: auto;
    /* width: 360px; */
    /* height: 740px;   */
    /* display: flex; */
    /* flex-direction: column; */
    /* align-items: center; */
    
    /* position: relative;
    z-index: 1; */
    border-radius: 25px;
    margin-top: 1.5rem;
    margin-bottom: 1.5rem;
    min-width: 310px;
    min-height: 660px;  
    max-width: 310px;
    max-height: 660px;  
    background-color: white;
    
    /* height: 739px; */
  }
}

.testeDiv {

  /* margin-top: -30px; */
  display: flex;
  flex-direction: column;
  align-items: center;
  
  @media screen and (min-width: 527px) {
    /* margin-top: -30px; */
    display: flex;
    flex-direction: column;
    align-items: center;
    min-width: 310px;
    min-height: 660px;  
    max-width: 310px;
    margin-top: 1.5rem;
    margin-bottom: 1.5rem;
    max-height: 660px;    
    background-color: white;
    border-radius: 25px;

  }
  
}


/* @media screen and (min-width: 527px) {

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
} */

</style>
