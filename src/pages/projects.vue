<template>
    <h1 class="text-grey">Projects</h1>
    <div class="ma-8">
      <v-expansion-panels variant="accordion">
        <v-expansion-panel v-for="project in myProjects" :key="project.title">
          <v-expansion-panel-title>{{ project.title }}</v-expansion-panel-title>
          <v-expansion-panel-text>
            <v-card>
              <v-card-text class="px-4 text-grey">
                <div class="font-weight-bold">de termijn {{ project.due }}</div>
                <div>{{ project.content }}</div>
              </v-card-text>
            </v-card>
          </v-expansion-panel-text>
        </v-expansion-panel>
      </v-expansion-panels>
    </div>
</template>

<script lang="ts">
  import { defineComponent, ref } from "vue";
  import type { ProjectInterface } from "@/interfaces/projectInterface"

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

      const myProjects = ref<ProjectInterface[]>([]);



      const sortByTitle = () => {
        projects.value.sort((a, b) => a.title.localeCompare(b.title));
      };

      const sortByPerson = () => {
        projects.value.sort((a, b) => a.person.localeCompare(b.person));
      };

      myProjects.value = projects.value.filter(item => item.person === "Shen Gongbao");

      return {
        projects,
        sortByTitle,
        sortByPerson,
        myProjects
      };   
    },
  });
</script>