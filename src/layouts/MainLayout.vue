<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title class="text-subtitle1">Juego de dados para adultos</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered content-class="bg-grey-1">
      <q-list>
        <q-item-label header class="text-grey-8">Configurar</q-item-label>
        <q-tree
          :nodes="navItems"
          node-key="Id"
          label-key="label"
          :selected.sync="menuselected"
          @update:selected="runLand"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <component v-bind:is="miContenido"  v-bind:inicial="inicial"/>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: "MainLayout",
  components: {
    PageIndex: () => import("pages/Index.vue"),
    Jugadores: () => import("pages/Jugadores.vue"),
    Dados: () => import("pages/Dados"),
    DadosConfig: () => import("pages/DadosConfig")
  },
  data() {
    return {
      miContenido: "PageIndex",
      leftDrawerOpen: false,
      menuselected: null,
      inicial:true,
    };
  },
  mounted() {
    this.$root.$on("goHome", () => {
      this.inicial=false;
      this.miContenido = "PageIndex";
    });
  },
  computed: {
    navItems() {
      return [
        {
          label: "Jugadores",
          icon: "people_alt",
          link: "Jugadores",
          Id: 0
        },
        {
          label: "Especificar dados",
          icon: "casino",
          link: "Dados",
          Id: 1
        },
        {
          label: "Configurar dados",
          icon: "explore",
          link: "DadosConfig",
          Id: 2
        }
      ];
    }
  },
  methods: {
    runLand(option) {
      this.leftDrawerOpen=false;
      this.miContenido = this.navItems[option].link;
      this.menuselected=null;
    }
  },
  // beforeDestroy () {
  //     localStorage.removeItem('jugadores');
  //     localStorage.removeItem('aJugadores');
  // }
};
</script>