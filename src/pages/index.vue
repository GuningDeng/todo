<template>
  <h1 class="text-grey">Taken overzicht</h1> 
  <v-container fluid class="my-5">
    <v-layout row justify-start class="mb-3">
      <v-btn small flat color="grey" @click="sortByTitle">
        <v-icon left small>mdi-folder</v-icon>
        <span class="text-lowercase">sorteren op naam</span>
        <v-tooltip activator="parent" location="top">
          <span>opnieuw ordenen</span>
        </v-tooltip>
    </v-btn>
    <v-btn small flat color="grey" @click="sortByPerson" class="ml-3">
      <v-icon left small>mdi-account</v-icon>
      <span class="text-lowercase">sorteren op persoon</span>
      <v-tooltip activator="parent" location="top">
        <span>opnieuw ordenen per verantwoordelijke persoon</span>
      </v-tooltip>
    </v-btn>
    </v-layout>

    <v-card flat v-for="project in projects" :key="project.title">
      <v-layout :class="`pa-3 project ${project.status}`">
        <v-row wrap>
          <v-col cols="6">
            <div class="text-caption text-grey">Naam van taak</div>
            <div>{{ project.title }}</div>
          </v-col>
          <v-col cols="2">
            <div class="text-caption text-grey">verantwoordelijke persoon</div>
            <div>{{ project.person }}</div>
          </v-col>
          <v-col cols="2">
            <div class="text-caption text-grey">de termijn</div>
            <div>{{ project.due }}</div>
          </v-col>
          <v-col cols="2">
            <div class="text-caption text-grey">status</div>
            <v-chip :class="`${project.status} text-white my-2`">
              {{ project.status }}
            </v-chip>
          </v-col>
        </v-row>
      </v-layout>
      <v-divider />

    </v-card>
  </v-container>   
</template>

<script lang="ts">
  import { defineComponent, ref } from "vue";
  import type { ProjectInterface } from "@/interfaces/projectInterface";

  export default defineComponent({
    setup() {
      const projects = ref<ProjectInterface[]>([
        {
          title: "Ontwerp een nieuw thema voor website",
          person: "Shen Gongbao",
          due: "2025-3-3",
          status: "overdue",
          content:
            "Ontwerp een nieuw websitethema voor klant XXC, inclusief startpagina, productpagina, informatiepagina en andere pagina's.",
        },
        {
          title: "Productweergave op de homepagina",
          person: "Nezha",
          due: "2025-3-12",
          status: "complete",
          content:
            "Gebruiker wil product showcases op de startpagina zien. Implementeer deze functionaliteit.",
        },
        {
          title: "Producten worden op productpagina weergegeven",
          person: "Ao Bing",
          due: "2025-3-24",
          status: "ongoing",
          content:
            "Gebruiker wil producten op productpagina zien. Implementeer deze functionaliteit.",
        },
        {
          title: "Testen",
          person: "Yin Furen",
          due: "2025-4-2",
          status: "overdue",
          content:
            "Test nieuwe functionaliteiten van het product om de product stabiliteit te garanderen.",
        },
      ]);

      const sortByTitle = () => {
        projects.value.sort((a, b) => a.title.localeCompare(b.title));
      };

      const sortByPerson = () => {
        projects.value.sort((a, b) => a.person.localeCompare(b.person));
      };

      return {
        projects,
        sortByTitle,
        sortByPerson,
      };   
    },
  });
    
</script>

<style scoped>
.project.complete {
  border-left: 4px solid #3cd1c2;
}
.project.ongoing {
  border-left: 4px solid #ffaa2c;
}
.project.overdue {
  border-left: 4px solid #f83e70;
}
.v-chip.complete {
  background: #3cd1c2;
}
.v-chip.ongoing {
  background: #ffaa2c;
}
.v-chip.overdue {
  background: #f83e70;
}
</style>
