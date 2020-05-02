<template>
    <q-page class="flex fit">
        <div class="row q-pa-sm items-start full-width">
        <q-card flat bordered class="my-card bg-grey-1 full-width q-px-sm">
            <q-card-section>
                <div class="row full-width">
                    <div class="col-12">
                         <q-input
                            v-model="NombreJugador"
                            ref="NombreJugador"
                            :rules="[() => !!NombreJugador || 'Por favor ingrese el nombre',
                                        () => !!NombreJugador && NombreJugador.length > 2 || 'Deber ser mayor a 2 caracteres' ]"
                            lazy-rules
                            input-style="min-width: 200px"
                            outlined
                            class="col"
                            label="Nombre del jugador:"
                            placeholder="Ingrese el nombre del jugador"
                            maxlength="30"
                            counter
                            standout
                            required
                            autocomplete="off"
                          >
                            <template v-slot:append>
                              <q-icon
                                v-if="NombreJugador"
                                @click="NombreJugador=''"
                                name="close"
                                class="cursor-pointer"
                              />
                            </template>
                          </q-input>
                    </div>
                </div>
                <div class="row full-width">
                    <div class="col-12">
                        <q-btn
                            no-caps
                            color="teal"
                            icon-right="add_circle_outline"
                            @click="Add()"
                            class="full-width text-subtitle1 myH"
                        > 
                        </q-btn>
                    </div>
                </div>
            </q-card-section>
            <q-card-section>
                 <div class="row full-width">
                    <div class="col-12">
                         <q-list>
                              <q-item-label header class="bg-blue-2 text-black">Lista de Jugadores</q-item-label>
                            <q-item
                                v-for="(jugador, index) in aJugadores"
                                :key="jugador"
                                tabindex="0" >
                                <q-item-section>{{jugador}}</q-item-section>
                                <q-item-section side >
                                   <q-btn
                                        no-caps
                                        color="orange"
                                        icon="remove_circle_outline"
                                        @click="Remove(index)"
                                    > 
                                    </q-btn>
                                </q-item-section>
                            </q-item>
                         </q-list>
                    </div>
                 </div>
            </q-card-section>
            <q-card-actions>
                <div class="row full-width">
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-pr-xs q-py-xs">
                        <q-btn
                            no-caps
                            color="teal"
                            icon-right="send"
                            @click="process(true)"
                            class="full-width text-subtitle1 myH"
                        > 
                        </q-btn>
                    </div>
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-pl-xs q-py-xs">
                        <q-btn
                            no-caps
                            color="purple-3"
                            icon-right="backspace"
                            @click="process(false)"
                            class="full-width text-subtitle1 myH"
                        > 
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
    name: 'Jugadores',
    data() {
        return {
            NombreJugador:'',
            aJugadores:[],
        }
    },
    mounted() {
        this.aJugadores=JSON.parse(localStorage.jugadoresnombres);
    },
    methods:
    {
        process(update) {
            if( update) {
                if( this.aJugadores.length > 1 ) {
                    localStorage.jugadores = this.aJugadores.length;
                    localStorage.jugadoresnombres = JSON.stringify(this.aJugadores);
                } else  {
                    this.$q.notify({
                    message: "Mínimo 2 jugadores",
                    caption: "Estimado usuario",
                    color: "pink-6",
                    position: "bottom-right",
                    icon: "info",
                    textColor: "white",
                    html: true,
                    timeout: 3000})
                    return
                }
            }
            this.$root.$emit("goHome");
        },
        Add(){
            if( this.aJugadores.length > 15 ) {
                this.$q.notify({
                message: "Máximo 16 jugadores",
                caption: "Estimado usuario",
                color: "pink-6",
                position: "bottom-right",
                icon: "info",
                textColor: "white",
                html: true,
                timeout: 3000})
            } else  {
                this.$refs.NombreJugador.validate()
                if( ! this.$refs.NombreJugador.hasError ) {
                    this.aJugadores.push( this.NombreJugador)
                    this.NombreJugador=''
                    this.$refs.NombreJugador.resetValidation()
                }
            }
        },
        Remove(jugador){
            this.aJugadores.splice(jugador,1)
        },
    }

}
</script>
<style >
.myH {
  height: 48px;
}
</style>