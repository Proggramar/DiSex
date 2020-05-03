<template>
  <q-page class="flex fit">
    <div class="row q-pa-sm items-start full-width">
      <q-card flat bordered class="my-card bg-grey-1 full-width q-px-sm">
        <q-card-section v-show="jugadorTurno!=99"
          class="bg-blue-4 text-white text-subtitle1 "
          >
            Lanzamiento de: {{ aJugadores[jugadorTurno] }}
        </q-card-section>
        <q-card-section v-show="jugadorTurno==99"
          class="bg-blue-4 text-white text-h6"
          >
            En espera del lanzamiento...
        </q-card-section>
        <q-card-section>
          <div v-for="dado in aTurnoLanzado" :key="dado.Dado" >
             <div class="row q-mb-md">
               <div class="col-4 bg-teal-3 text-black text-subtitle2 q-mb-none q-py-sm q-pr-sm vertical-middle" align="right">
                    {{dado.Dado}} :
                </div><div class="col-8 bg-orange-2 text-black text-subtitle3 text-bold q-mb-none q-py-sm q-pl-sm vertical-middle" align="left">
                    {{dado.Accion}}
                </div>
             </div>
          </div>
        </q-card-section>
       
         <q-card-actions >
          <div class="row full-width">
            <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-py-xs">
              <q-btn
                no-caps
                color="teal"
                icon-right="slideshow"
                @click="frmLanzar(true)"
                class="full-width text-subtitle1 myH"
              >
              {{aJugadores[jugadorNext] }} 
              </q-btn>
            </div>
            <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-py-xs" v-show="playing">
              <q-btn
                no-caps
                color="purple-3"
                icon-right="replay"
                @click="frmLanzar(false)"
                class="full-width text-subtitle1 myH"
              >
              {{aJugadores[jugadorTurno] }} 
              </q-btn>
            </div>
          </div>
        </q-card-actions>
      </q-card>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  props: ['inicial'],
  data() {
    return {
      jugadores: 2,
      jugadorTurno: 99,
      jugadorNext:0,
      aJugadores: ["Jugador 1","Jugador 2"],
      aDados: [0,1,2,3,4,5,6,7,8],
      aNombresDados: ["Acción","Zona","Tiempo","Prenda","Licor","Penitencia","Acción por","Experto","Maestro"],
      aConfigDados: [
        ["Lamer/Chupar","Besar","Mordizquear","Acariciar","Acariciar y Besar","Libre"],
        ["Cuello","Oreja","Espalda","Ombligo","Muslo","Libre"],
        ["1 min","5 seg","10 seg","20 seg","30 seg","40 seg"],
        ["Recupera 1","Pierde 1","Pierde 2","Todos pierden 1","Todos recuperan 1","Recupera 2"],
        ["Libre","Toma 1","Toma 2","Todos toman 1","Todos toman 2","No toma"],
        ["Vuelve a lanzar","Recibe 1","Recibe 2","Coloca 1","Coloca 2","Libre"],
        ["Todos","Jugador de la derecha","Jugador de la izquierda","2do Jugador de la derecha","2do Jugador de la izquieda","Salvado de las acciones"],
        ["Desnudo(a) hasta siguiente turno","Doble tiempo","Doble prenda","Doble penitencia","Todos desnudos 1 turno","Pasa acción a jugador...",],
        ["Besar zona intima","Beso con lengua","Besar las nalgas","Besar cuerpo (20 seg)","Chupar los pezones","Acción y Zona libre (1 min)"]
      ],
      aTurnoLanzado:[],
      playing: false,
    };
  },
  mounted() {
    // valida el localstorage
    if (localStorage.dados) {
      this.LoadData();
    } else {
      this.SetData();
      this.ShowHow();
    }
    this.$root.$on("Update", (procesar) => {
       switch( procesar.accion) {
         case "jugadores":
           this.jugadores=procesar.jugadores
           this.aJugadores=procesar.nombres
           break
       }
    });
  },
  methods: {
    ShowHow() {
      const dialog = this.$q
          .dialog({
            title: "Para jugar DiSex<em>!</em>",
            message: "Primero debe:<br><br>1. Abrir el menu del panel izquierdo.<br>2. Especificar los jugadores.<br>" +
                     "3. Definir la cantidad de dados con los que van a jugar.<br>"+
                     "4. Cambiar las especificaciones de los dados (si lo desea).",
            html: true,
            ok: {
              color: "primary"
            },
            persistent: true
          })
          
          .onDismiss(() => {
            clearTimeout(timer);
          });
        const timer = setTimeout(() => {
          dialog.hide();
        }, 30000);
    },
    LoadData() {
      this.aDados = JSON.parse(localStorage.dados);
      this.aNombresDados = JSON.parse(localStorage.dadosnombres);
      this.aConfigDados = JSON.parse(localStorage.dadosconfig);
      if( ! this.inicial) {
        this.jugadores=localStorage.jugadores;
        this.aJugadores=JSON.parse(localStorage.jugadoresnombres);
      } else {
        localStorage.removeItem('jugadores');
        localStorage.removeItem('jugadoresnombres');
        localStorage.jugadores = this.jugadores;
        localStorage.jugadoresnombres = JSON.stringify(this.aJugadores);
      }
      
    },
    SetData() {
      localStorage.jugadores = this.jugadores;
      localStorage.jugadoresnombres = JSON.stringify(this.aJugadores);
      localStorage.dados = JSON.stringify(this.aDados);
      localStorage.dadosnombres = JSON.stringify(this.aNombresDados);
      localStorage.dadosconfig = JSON.stringify(this.aConfigDados);
    },
    frmLanzar(lPrimeroAvanzaJugador) {
      this.playing=true
      if (lPrimeroAvanzaJugador) { 
        this.jugadorTurno++; 
        this.jugadorNext++
      }
      if (this.jugadorTurno >= this.jugadores) this.jugadorTurno = 0;
      if (this.jugadorNext >= this.jugadores) this.jugadorNext = 0;
      this.LanzarDados();
      window.scrollTo(0, 0);
    },
    LanzarDados() {
      // generar turnos aleatorios para cada dado
      let aDado={}
      let nLanzado=0
      this.aTurnoLanzado=[]
      this.aDados.map((value) => {
        aDado = {'Id': value,
                'Dado' : this.aNombresDados[value], 
                'Turnos' : this.NumeroAleatorio(1, 100),
                'Lanzado':0,
                'Accion':''}
        this.aTurnoLanzado.push(aDado)
      })
      this.aTurnoLanzado.map( (value, index) => {
          for(var nLanzando=0; nLanzando< value.Turnos; nLanzando++) {
            nLanzado=this.NumeroAleatorio(1, 6)
            this.aTurnoLanzado[index].Lanzado=nLanzado
          }
          this.aTurnoLanzado[index].Accion=this.aConfigDados[value.Id][nLanzado-1]
      } )
    },
    NumeroAleatorio(menor, mayor) {
      let n = 0;
      let nIntentos = Math.floor(Math.random() * (10 - 1 + 1) + 1);
      
      for (var nItera = 0; nItera < nIntentos; nItera++) {
        n = Math.floor(Math.random() * (mayor - menor + 1) + menor);
      }
      return n;
    }
  }
};
</script>
<style >
.miColumn {
  height: 800px !important;
}
.myH {
  height: 48px;
}

</style>