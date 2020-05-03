<template>
    <q-page class="flex fit">
        <div class="row q-pa-sm items-start full-width">
        <q-card flat bordered class="my-card bg-grey-1 full-width q-px-sm">
            <q-card-section>
                <div class="row full-width">
                    <div class="col-12">
                        <q-select
                            clearable
                            v-model="sDadoConfig"
                            :options="aDados"
                            label="Seleccione el Dado:"
                            transition-show="flip-up"
                            transition-hide="flip-down"
                            outlined 
                            color="blue"  
                            label-color="blue"
                            :display-value="`${sDadoConfig ? sDadoConfig : 'Por favor seleccione el dado'}`"
                            @input="SeleccionoDado"
                            />
                    </div>
                </div>
            </q-card-section>
            <q-card-section>
                <div class="row q-mb-md">
                    <div class="col-12 q-mb-sm q-pr-xs">
                         <q-input
                            v-model="NombreDado"
                            ref="NombreDado"
                            :rules="[() => !!Nombre3 || 'Dato requerido',
                                        () => !!Nombre3 && Nombre3.length > 2 || 'Deber ser mayor a 2 caracteres' ]"
                            lazy-rules
                            input-style="min-width: 200px"
                            outlined
                            class="col"
                            label="Nombre Dado:"
                            maxlength="30"
                            counter
                            standout
                            required
                            autocomplete="off"
                          >
                            <template v-slot:append>
                              <q-icon
                                v-if="NombreDado"
                                @click="NombreDado=''"
                                name="close"
                                class="cursor-pointer"
                              />
                            </template>
                          </q-input>
                    </div>
                </div>
                <div class="row q-mb-md">
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-mb-sm q-pr-xs">
                         <q-input
                            v-model="Nombre1"
                            ref="Nombre1"
                            :rules="[() => !!Nombre1 || 'Dato requerido',
                                        () => !!Nombre1 && Nombre1.length > 2 || 'Deber ser mayor a 2 caracteres' ]"
                            lazy-rules
                            input-style="min-width: 200px"
                            outlined
                            class="col"
                            label="Cara 1 :"
                            maxlength="30"
                            counter
                            standout
                            required
                            autocomplete="off"
                          >
                            <template v-slot:append>
                              <q-icon
                                v-if="Nombre1"
                                @click="Nombre1=''"
                                name="close"
                                class="cursor-pointer"
                              />
                            </template>
                          </q-input>
                    </div>
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-mb-sm q-pr-xs">
                        <q-input
                            v-model="Nombre2"
                            ref="Nombre2"
                            :rules="[() => !!Nombre2 || 'Dato requerido',
                                        () => !!Nombre2 && Nombre2.length > 2 || 'Deber ser mayor a 2 caracteres' ]"
                            lazy-rules
                            input-style="min-width: 200px"
                            outlined
                            class="col"
                            label="Cara 2 :"
                            maxlength="30"
                            counter
                            standout
                            required
                            autocomplete="off"
                          >
                            <template v-slot:append>
                              <q-icon
                                v-if="Nombre2"
                                @click="Nombre2=''"
                                name="close"
                                class="cursor-pointer"
                              />
                            </template>
                          </q-input>
                    </div>
                </div>
                <div class="row q-mb-md">
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-mb-sm q-pr-xs">
                         <q-input
                            v-model="Nombre3"
                            ref="Nombre3"
                            :rules="[() => !!Nombre3 || 'Dato requerido',
                                        () => !!Nombre3 && Nombre3.length > 2 || 'Deber ser mayor a 2 caracteres' ]"
                            lazy-rules
                            input-style="min-width: 200px"
                            outlined
                            class="col"
                            label="Cara 3 :"
                            maxlength="30"
                            counter
                            standout
                            required
                            autocomplete="off"
                          >
                            <template v-slot:append>
                              <q-icon
                                v-if="Nombre3"
                                @click="Nombre3=''"
                                name="close"
                                class="cursor-pointer"
                              />
                            </template>
                          </q-input>
                    </div>
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-mb-sm q-pr-xs">
                        <q-input
                            v-model="Nombre4"
                            ref="Nombre4"
                            :rules="[() => !!Nombre4 || 'Dato requerido',
                                        () => !!Nombre4 && Nombre4.length > 2 || 'Deber ser mayor a 2 caracteres' ]"
                            lazy-rules
                            input-style="min-width: 200px"
                            outlined
                            class="col"
                            label="Cara 4 :"
                            maxlength="30"
                            counter
                            standout
                            required
                            autocomplete="off"
                          >
                            <template v-slot:append>
                              <q-icon
                                v-if="Nombre4"
                                @click="Nombre4=''"
                                name="close"
                                class="cursor-pointer"
                              />
                            </template>
                          </q-input>
                    </div>
                </div>
                <div class="row q-mb-md">
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-mb-sm q-pr-xs">
                         <q-input
                            v-model="Nombre5"
                            ref="Nombre5"
                            :rules="[() => !!Nombre5 || 'Dato requerido',
                                        () => !!Nombre5 && Nombre5.length > 2 || 'Deber ser mayor a 2 caracteres' ]"
                            lazy-rules
                            input-style="min-width: 200px"
                            outlined
                            class="col"
                            label="Cara 5 :"
                            maxlength="30"
                            counter
                            standout
                            required
                            autocomplete="off"
                          >
                            <template v-slot:append>
                              <q-icon
                                v-if="Nombre5"
                                @click="Nombre5=''"
                                name="close"
                                class="cursor-pointer"
                              />
                            </template>
                          </q-input>
                    </div>
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-mb-sm q-pr-xs">
                        <q-input
                            v-model="Nombre6"
                            ref="Nombre6"
                            :rules="[() => !!Nombre6 || 'Dato requerido',
                                        () => !!Nombre6 && Nombre6.length > 2 || 'Deber ser mayor a 2 caracteres' ]"
                            lazy-rules
                            input-style="min-width: 200px"
                            outlined
                            class="col"
                            label="Cara 6 :"
                            maxlength="30"
                            counter
                            standout
                            required
                            autocomplete="off"
                          >
                            <template v-slot:append>
                              <q-icon
                                v-if="Nombre6"
                                @click="Nombre6=''"
                                name="close"
                                class="cursor-pointer"
                              />
                            </template>
                          </q-input>
                    </div>
                </div>
                 <div class="row q-mb-md">
                    <div class="col-xs-12 col-sm-6 col-md-6 col-lg-6 col-xl-6 q-mb-sm q-pr-xs">
                         <q-btn
                            no-caps
                            color="orange"
                            icon-right="refresh"
                            @click="update()"
                            class="full-width text-subtitle1 myH"
                        > 
                        </q-btn>
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
    name: 'DadosConfig',
    data() {
        return {
            sDadoConfig: null,
            aDados:[],
            aDadosAcciones:[],
            NombreDado:"",
            Nombre1:"",
            Nombre2:"",
            Nombre3:"",
            Nombre4:"",
            Nombre5:"",
            Nombre6:"",
            nPosDado: null,
        }
    },
    mounted() {
        this.aDados=JSON.parse(localStorage.dadosnombres);
        this.aDadosAcciones=JSON.parse(localStorage.dadosconfig);
        
    },
    methods:
    {
        process(update) {
            if( update) {
                localStorage.dadosconfig =JSON.stringify(this.aDadosAcciones)
                localStorage.dadosnombres =JSON.stringify(this.aDados)
            }
            this.$root.$emit("goHome");
        },
        SeleccionoDado() {
            if( this.sDadoConfig !== null) {
                let nDado= this.aDados.indexOf(this.sDadoConfig)
                this.NombreDado=this.sDadoConfig;
                this.Nombre1=this.aDadosAcciones[nDado][0]
                this.Nombre2=this.aDadosAcciones[nDado][1]
                this.Nombre3=this.aDadosAcciones[nDado][2]
                this.Nombre4=this.aDadosAcciones[nDado][3]
                this.Nombre5=this.aDadosAcciones[nDado][4]
                this.Nombre6=this.aDadosAcciones[nDado][5]
                this.clearvalidatees()
                this.nPosDado=nDado
            } else {
                this.clear()
            }
        },
        update() {
            this.$refs.NombreDado.validate()
            this.$refs.Nombre1.validate()
            this.$refs.Nombre2.validate()
            this.$refs.Nombre3.validate()
            this.$refs.Nombre4.validate()
            this.$refs.Nombre5.validate()
            this.$refs.Nombre6.validate()
            if( ! ( this.$refs.Nombre1.hasError || this.$refs.Nombre2.hasError
                    || this.$refs.Nombre3.hasError || this.$refs.Nombre4.hasError
                    || this.$refs.Nombre5.hasError || this.$refs.Nombre6.hasError
                    || this.$refs.NombreDado.hasError ) ) { 
                        this.aDadosAcciones[this.nPosDado][0]=this.Nombre1
                        this.aDadosAcciones[this.nPosDado][1]=this.Nombre2
                        this.aDadosAcciones[this.nPosDado][2]=this.Nombre3
                        this.aDadosAcciones[this.nPosDado][3]=this.Nombre4
                        this.aDadosAcciones[this.nPosDado][4]=this.Nombre5
                        this.aDadosAcciones[this.nPosDado][5]=this.Nombre6
                        this.aDados[this.nPosDado]=this.NombreDado
                        this.clear()
                        this.sDadoConfig= null
            } else {
                this.$q.notify({
                message: "Primero debe llenar los datos de todas las caras del dado",
                caption: "Estimado usuario",
                color: "pink-6",
                position: "bottom-right",
                icon: "info",
                textColor: "white",
                html: true,
                timeout: 3000
            });
            }
        },
        clear() {
          this.NombreDado=''
          this.Nombre1=''
          this.Nombre2=''
          this.Nombre3=''
          this.Nombre4=''
          this.Nombre5=''
          this.Nombre6=''
          this.clearvalidatees()
        },
        clearvalidatees() {
            this.$refs.NombreDado.resetValidation()
            this.$refs.Nombre1.resetValidation()
            this.$refs.Nombre2.resetValidation()
            this.$refs.Nombre3.resetValidation()
            this.$refs.Nombre4.resetValidation()
            this.$refs.Nombre5.resetValidation()
            this.$refs.Nombre6.resetValidation()
        },
        
    }

}
</script>
<style >
.myH {
  height: 48px;
}
</style>