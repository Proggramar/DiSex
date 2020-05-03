<template>
    <q-page class="flex fit">
        <div class="row q-pa-sm items-start full-width">
        <q-card flat bordered class="my-card bg-grey-1 full-width q-px-sm">
            <q-card-section>
                <div class="row full-width">
                    <div class="col-12">
                        <q-list>
                            <q-item-label header class="bg-blue-2 text-black">Dados disponibles</q-item-label>
                            <q-item
                                v-for="(dadod,index) in aDadosDisponibles"
                                :key="dadod"
                                tabindex="0" >
                                <q-item-section>{{dadod}}</q-item-section>
                                <q-item-section side >
                                    <q-btn
                                        no-caps
                                        color="orange"
                                        icon="add_circle_outline"
                                        @click="Add(dadod, index)"
                                    > 
                                    </q-btn>
                                </q-item-section>
                            </q-item>
                        </q-list>
                    </div>
                </div>
            </q-card-section>
            <q-card-section>
                 <div class="row full-width">
                    <div class="col-12">
                         <q-list>
                              <q-item-label header class="bg-blue-2 text-black">Dados a lanzar</q-item-label>
                            <q-item
                                v-for="(dado, index) in aDados"
                                :key="dado"
                                tabindex="0" >
                                <q-item-section>{{dado}}</q-item-section>
                                <q-item-section side >
                                   <q-btn
                                        no-caps
                                        color="orange"
                                        icon="remove_circle_outline"
                                        @click="Remove(dado,index)"
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
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-py-xs">
                        <q-btn
                            no-caps
                            color="teal"
                            icon-right="send"
                            @click="process(true)"
                            class="full-width text-subtitle1 myH"
                        > 
                        </q-btn>
                    </div>
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-py-xs">
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
    name: 'Dados',
    data() {
        return {
            aDados:[],
            aDadosDisponibles:[],
            aDadosNombres:[],
        }
    },
    mounted() {
        this.aDadosNombres=JSON.parse(localStorage.dadosnombres);
        let aDadosIndex=JSON.parse(localStorage.dados);
        this.aDadosNombres.map( (nombre,index)=>{
            if( aDadosIndex.includes(index)) {
                this.aDados.push(nombre)
            } else {
                this.aDadosDisponibles.push(nombre)
            }
        } )

    },
    methods:
    {
        process(update) {
            if( update) {
                let aDadosSeleccionados=[]
                this.aDados.map(dado => {
                    aDadosSeleccionados.push( this.aDadosNombres.indexOf(dado))
                })
                localStorage.dados =JSON.stringify(aDadosSeleccionados)
            }
            this.$root.$emit("goHome");
        },
        Add(dado, index){
            this.aDados.push(dado)
            this.aDadosDisponibles.splice(index,1)
           
        },
        Remove(dado, index){
            this.aDados.splice(index,1)
             this.aDadosDisponibles.push(dado)
        },
    }

}
</script>
<style >
.myH {
  height: 48px;
}
</style>