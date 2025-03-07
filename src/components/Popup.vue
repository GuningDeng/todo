<template>
    <v-dialog max-width="600" v-model="dialog">
      <template v-slot:activator="{ props: activatorProps }">
        <v-btn
          v-bind="activatorProps"
          color="success"
          text="Nieuwe taken"
          variant="flat"
        ></v-btn>
      </template>
  
      <template v-slot:default="{ isActive }">
        <v-card title="Nieuwe taak toevoegen">
          <v-card-text>
            <v-form class="px-3" @submit.prevent>
              <v-text-field
                v-model="form_data.title"
                label="Naam"
                prepend-icon="mdi-folder"
                :rules="[rules.required, rules.min, rules.max]"
              ></v-text-field>
              <v-textarea
                v-model="form_data.content"
                label="Details"
                prepend-icon="mdi-note"
                :rules="[rules.required, rules.min, rules.max]"
              ></v-textarea>
  
              <v-menu v-model="menu" :close-on-content-click="false">
                <template v-slot:activator="{ props }">
                  <v-text-field
                    v-model="formatedDate"
                    label="De termijn"
                    prepend-icon="mdi-calendar-month"
                    v-bind="props"
                    readonly
                  ></v-text-field>
                </template>
                <v-date-picker v-model="form_data.due"></v-date-picker>
              </v-menu>
  
              <div align="right" class="mt-4">
                <v-btn
                  type="submit"
                  flat
                  @click="submit"
                  color="success"
                  :loading="loading"
                  ><span>Opslaan</span></v-btn
                >
                <v-btn
                  flat
                  text="Sluiten"
                  @click="isActive.value = false"
                  class="ml-2"
                ></v-btn>
              </div>
            </v-form>
          </v-card-text>
        </v-card>
      </template>
    </v-dialog>
  </template>
  
  <script setup>
  
  import { ref, computed, watch, defineEmits} from "vue";
  import format from "date-fns/format";
  
  const projects = ref([
    {
        title: "Ontwerp een nieuw thema voor website",
        person: "Shen Gongbao",
        due: "2025-3-3",
        status: "overdue",
        content: "Ontwerp een nieuw websitethema voor klant XXC, inclusief startpagina, productpagina, informatiepagina en andere pagina's.",
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
        content: "Gebruiker wil producten op productpagina zien. Implementeer deze functionaliteit.",
    },
    {
        title: "Testen",
        person: "Yīn Furen",
        due: "2025-4-2",
        status: "overdue",
        content: "Test nieuwe functionaliteiten van het product om de product stabiliteit te garanderen.",
    },
  ])
  
  const form_data = ref({
    title: "",
    content: "",
    due: null,
  });
  
  const loading = ref(false);
  const dialog = ref(false);
  const menu = ref(false);
  
  //Monitor due data changes and close the menu if it changes
  watch(
    () => form_data.value.due,
    () => {
      menu.value = false;
    }
  );
  
  // Formatting Dates
  const formatedDate = computed(() => {
    if (form_data.value && form_data.value.due) {
      //console.log(form_data.value.due);
      return format(form_data.value.due, "yyyy-MM-dd");
    } else {
      return "";
    }
  });
  
  //Verification
  const rules = {
    required: (value) => !!value || "Cannot be empty",
    min: (value) => value.length >= 3 || "Minimum 3 characters",
    max: (value) => value.length <= 20 || "Maximum 20 characters",
  };
  
  const emits = defineEmits(["projectAdded"]);
  
  const submit = () => {
    loading.value = true;
  
    if (
      !form_data.value.title ||
      !form_data.value.content ||
      !form_data.value.due
    ) {
      loading.value = false;
      return;
    }
  
    const newProject = {
      title: form_data.value.title,
      content: form_data.value.content,
      person: "sheng gongbao",
      due: format(form_data.value.due, "yyyy-MM-dd"),
      status: "ongoing",
    };
  
    projects.value.push(newProject);

    // projects(newProject)
    //   .then(() => {
    //     console.log("Taak succesvol toegevoegd！");
    //     console.log(JSON.stringify(form_data.value));
    //     loading.value = false;
    //     dialog.value = false;
    //     emits("projectAdded");
    //   })
    //   .catch((error) => {
    //     console.error("Error writing document: ", error);
    //     loading.value = false;
    //   });
  };
  </script>