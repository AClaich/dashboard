<script setup lang="ts">
import { ref, onMounted } from 'vue';
import axios from "axios";


export interface UserEntity {
  id: number;
  attributes: UserAttributes;
}

export interface UserAttributes {
  prenom: string;
  nom: string;
  email: string;
  password: string;
  number: number;
  can_invite: number;
  is_vin: number;
  is_reception: number;
  is_retour: number;
  presence_vin_1: number;
  presence_reception_1: number;
  presence_retour_1: number;
  presence_vin_2: number;
  presence_reception_2: number;
  presence_retour_2: number;
  vegetarien_1: number;
  logement_1: number;
  vegetarien_2: number;
  logement_2: number;
  jeudi_1: number;
  vendredi_1: number;
  samedi_1: number;
  jeudi_2: number;
  vendredi_2: number;
  samedi_2: number;
}

export interface LoginFormState {
  username: string;
  password: string;
}

const listUsers = ref<UserEntity[]>([]);

onMounted(async () => {
  try {
    const response = await axios.get(
      "https://www.fonkbox.fr/api/dataconnexions"
    );
    listUsers.value = response.data.data as UserEntity[];
  } catch (error) {
    console.error(error);
  }
});
</script>

<template>
  <a-layout class="layout">
    <a-layout-header class="header">
      <div>Test</div>
    </a-layout-header>
    <a-layout-content style="padding: 0 50px" class="site-layout-content">

      <div :style="{ background: '#fff', padding: '24px', minHeight: '280px' }">      {{ listUsers }}</div>
    </a-layout-content>
  </a-layout>
</template>

<style scoped>
.header-item {
  color: white;
}

.header {
  position: fixed;
  z-index: 1;
  width: 100%;
  background: #001529;
  color: white;
}

.site-layout-content {
  min-height: 280px;
  padding: 24px;
  background-color: #f5f5f5;
}

#components-layout-demo-top .logo {
  float: left;
  width: 120px;
  height: 31px;
  margin: 16px 24px 16px 0;
  background: rgba(255, 255, 255, 0.3);
}

.ant-row-rtl #components-layout-demo-top .logo {
  float: right;
  margin: 16px 0 16px 24px;
}

[data-theme='dark'] .site-layout-content {
  background: #141414;
}
</style>
