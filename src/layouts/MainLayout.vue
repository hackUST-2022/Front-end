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
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> {{ AppName }} </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
  {
    title: "Home",
    caption: window.location.href,
    icon: "home",
    link: window.location.href,
  },
  {
    title: "MIT master degree",
    caption: "gradadmissions.mit.edu/programs/degrees/masters-degrees",
    icon: "school",
    link: "https://gradadmissions.mit.edu/programs/degrees/masters-degrees",
  },
  {
    title: "Stanford school of engineering",
    caption: "gradadmissions.stanford.edu/school/school-engineering",
    icon: "school",
    link: "https://gradadmissions.stanford.edu/school/school-engineering",
  },
];

export default defineComponent({
  name: "MainLayout",
  data() {
    return {
      AppName: "School Application Helper"
    };
  },

  components: {
    EssentialLink,
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
