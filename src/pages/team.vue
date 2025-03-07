<template>
    <h1 class="text-grey">Team</h1>
    <v-container class="my-5">
        <v-row wrap>
      <v-col xs12 sm6 md4 lg3 v-for="person in team" :key="person.name">
        <v-card flat class="text-center ma-3" elevation="16">
          <v-responsive class="pt-4">
            <v-avatar size="100" color="grey">
              <img :src="person.avatar" />
            </v-avatar>
          </v-responsive>
          <v-card-text>
            <div class="text-subtitle-1">{{ person.name }}</div>
            <div class="text-grey">{{ person.role }}</div>
          </v-card-text>
          <v-card-actions>
            <v-btn flat color="grey">
              <v-icon>mdi-message</v-icon>
              <span>bericht</span>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    </v-container>
</template>

<script setup>
const team = [
  { name: "taiyi", role: "accountmanager", avatar: "/image/taiyi.jpg" },
  { name: "sheng gong bao", role: "programmeur", avatar: "/image/shen_gongbao.jpg" },
  { name: "nezha", role: "programmeur", avatar: "/image/nezha.jpg" },
  { name: "ao bing", role: "programmeur", avatar: "/image/ao_bing.jpg" },
  { name: "yin furen", role: "Tester", avatar: "/image/yin_furen.jpg" },
];

</script>