<template>
  <v-app>
    <!-- bar de navigation -->
    <v-app-bar class="px-3" color="grey-darken-4" flat density="compact">
      <v-spacer></v-spacer>
      <v-tabs v-model="selectedTab" centered color="grey-darken-1">
        <v-tab v-for="link in links" ::key="link">
          {{ link }}
        </v-tab>
      </v-tabs>
      <v-spacer></v-spacer>
    </v-app-bar>
    <!-- Container -->
     <v-main>
      <v-container fluid>
        <v-row>
          <!-- Left col -->
          <v-col cols="12" sm="2"></v-col>
          <!-- Main col -->
          <v-col cols="12" sm="8">
            <v-sheet
              v-if="selectedTab == 0"
              min-height="70vh"
              rounded="lg"
              class="pa-4"
            >
            <h2 class="mt-4">Apps list: </h2>
            {{ apiResult }}
          </v-sheet>
            <v-sheet
              v-else
              min-height="70vh"
              rounded="lg"
              class="pa-2 pt-4"
            >
          Page 1
          </v-sheet>
          </v-col>
          <!-- Right col -->
          <v-col cols="12" sm="2"></v-col>
        </v-row>
      </v-container>
     </v-main>
  </v-app>
</template>

<script lang="ts" setup>
import { ref, watch, onMounted } from 'vue';

let  selectedTab = ref(0)
const links = ref(["Dashbord", "About"])
let apiResult = ref()
let groupedData = ref([])

onMounted (async ( )=> {
  fetchMonetizationApi()
})

watch(apiResult, (newValue) =>{
  groupedData.value = useGroupApps(newValue.data)
})


// API
const fetchMonetizationApi = async () => {
  fetch('/monetization-api.json')
  .then(response => response.json())
  .then(data => apiResult.value = data)
}
</script>
