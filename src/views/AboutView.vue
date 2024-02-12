<template>
  <div class="about">
    <div class="nav">

      <b-button class="botaoVoltar" @click="voltar">
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
      <img class="flechaAzul" src="../views/flecha azul sentido.png" width="12px" height="12px" alt="Ícone" />
      <p class="saidaTrajeto">{{ this.ida ? this.linhaSelecionada.horarios.ida.trajeto.chegada :  this.linhaSelecionada.horarios.volta.trajeto.chegada}}</p>
      
      <b-button 
      class="flechas"
      @click="trocarSentidoRota"
      > 
        <img  src="../views/double-arrow.png" width="24px" height="24px" alt="Ícone" />
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
</template>



<script>

import { BButton } from 'bootstrap-vue'



export default {
  name: 'Horarios',
  data() {
    return {
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
    }
  },
  components: {
    BButton,
  },


  mounted() {
    const idLinha = this.$route.params.id;

    if (idLinha) {
      this.id = idLinha

    }
    console.log(this.id);




    let linhaFiltrada = this.linhas.filter(item => item.id == idLinha);
    if (linhaFiltrada.length > 0) {
      this.linha = linhaFiltrada[0].name;
      console.log(this.linha);
    }
    this.linhaSelecionada = this.rotas.find(rota => rota.id == this.id)


    if (this.ida) {
        this.horarios = this.linhaSelecionada.horarios.ida.horarios
        this.labelLinha = this.linhaSelecionada.horarios.ida.trajeto.label
      }else{
        this.horarios = this.linhaSelecionada.horarios.volta.horarios
        this.labelLinha = this.linhaSelecionada.horarios.volta.trajeto.label
      }
    console.log(this.linhaSelecionada)
  },

  computed: {

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
    voltar() {
      this.$router.go(-1);
    },
    trocarSentidoRota(){
      return this.ida = !this.ida
    },
  },

}
</script>

<style scoped>


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
  flex-direction: row;
}

.divColuna{
  display: flex;
  flex-direction: column;
}



.labelTrajeto{
  font-size: 14px;
  width: 150px;
}

.flechaAzul{
  margin: 5px 12px 0px 12px;
}
.flechas {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: transparent;
  border-color: transparent;
  margin-left: 10px;
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
}

.botaoVoltar {
  background-color: transparent;
  border-color: transparent;
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
  margin-top: 0.2rem;
  width: auto;
  height: 82px;
  background-color: #052144;
}
</style>
