<template>
  <v-app>
    <v-content>
      <v-container>
<!--        <ScrollTopComponent/>-->
          <WaterFallsFlowComponent/>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import NormalWatch from './components/NormalWatch'
import DeepWatch from './components/DeepWatch'
import DeepWatchForVar from './components/DeepWatchForVar'
import ScrollTopComponent from './components/ScrollTopComponent'
import WaterFallsFlowComponent from './components/WaterFallsFlowComponent'
export default {
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [
        { icon: 'bubble_chart', title: 'Inspire' }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  },
  components: {
    NormalWatch,
    DeepWatch,
    DeepWatchForVar,
    ScrollTopComponent,
      WaterFallsFlowComponent
  }
}
</script>
