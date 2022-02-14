<template>
  <q-layout view="lHr lpR fFf">
    <q-header bordered class="bg-white text-black">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class="text-weight-bold"
          ><span class="gt-sm">{{ $route.name }}</span>
          <q-icon
            class="q-pa-md lt-md header-icon"
            name="fab fa-twitter"
            size="lg"
            color="primary"
          />
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      show-if-above
      v-model="leftDrawerOpen"
      side="left"
      :width="283"
      bordered
    >
      <!-- drawer content -->
      <q-icon class="q-pa-md" name="fab fa-twitter" size="lg" color="primary" />
      <q-list>
        <q-item to="/" clickable v-ripple exact>
          <q-item-section avatar>
            <q-icon name="home" />
          </q-item-section>

          <q-item-section class="text-h6 text-weight-bold">Home</q-item-section>
        </q-item>
        <q-item to="/about" clickable v-ripple exact>
          <q-item-section avatar>
            <q-icon name="help" />
          </q-item-section>

          <q-item-section class="text-h6 text-weight-bold"
            >About</q-item-section
          >
        </q-item>
      </q-list>
      <!-- /drawer content -->
    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <!-- drawer content -->
      <q-input
        class="q-ma-md"
        placeholder="Search Qwitter"
        outlined
        rounded
        dense
      >
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>
      <q-list padding separator>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label class="text-gray" overline>Politics</q-item-label>
            <q-item-label class="text-weight-bold"
              >Lorem ipsum dolor</q-item-label
            >
            <q-item-label caption
              >Lorem ipsum dolor sit amet consectetur adipisicing elit. Aliquam
              nesciunt quidem, facilis.</q-item-label
            >
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label class="text-gray" overline>Education</q-item-label>
            <q-item-label class="text-weight-bold"
              >Consectetur adipisicing elit</q-item-label
            >
            <q-item-label caption
              >Lorem ipsum dolor sit amet consectetur adipisicing elit. Aliquam
              nesciunt quidem, facilis.</q-item-label
            >
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>6 min ago</q-item-label>
          </q-item-section>
        </q-item>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label class="text-gray" overline>Politics</q-item-label>
            <q-item-label class="text-weight-bold"
              >Aliquam nesciunt quidem</q-item-label
            >
            <q-item-label caption
              >Lorem ipsum dolor sit amet consectetur adipisicing elit. Aliquam
              nesciunt quidem, facilis.</q-item-label
            >
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>8 min ago</q-item-label>
          </q-item-section>
        </q-item>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label class="text-gray" overline>Science</q-item-label>
            <q-item-label class="text-weight-bold"
              >Sit amet consectetur</q-item-label
            >
            <q-item-label caption
              >Lorem ipsum dolor sit amet consectetur adipisicing elit. Aliquam
              nesciunt quidem, facilis.</q-item-label
            >
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>10 min ago</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
      <!-- /drawer content -->
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const rightDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },

      rightDrawerOpen,
      toggleRightDrawer() {
        rightDrawerOpen.value = !rightDrawerOpen.value;
      },
    };
  },
};
</script>

<style lang="scss">
.header-icon {
  position: absolute;
  bottom: 0;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
