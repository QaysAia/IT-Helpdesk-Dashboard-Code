<template>
  <q-layout view="hHh LpR fff" class="bg-grey-2">
    <q-header>
      <q-toolbar style="min-height: 57px">
        <q-btn
          class="text-white"
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
        <q-toolbar-title>
          <!-- <q-img
            style="height: 42px; width: 42px"
            src="~assets/logo.png"
            class="q-mr-md"
          ></q-img> -->
          <span v-if="$q.screen.gt.xs">Mi Task</span>
        </q-toolbar-title>

        <q-btn-dropdown color="q-dark" flat no-caps>
          <template v-slot:label>
            <div class="row items-center no-wrap">
              <q-avatar>
                <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
              </q-avatar>
              <div class="text-center q-pa-sm">qays</div>
            </div>
          </template>

          <q-list style="min-width: 300px">
            <q-item class="q-pa-md">
              <q-item-section class="text-center">
                <q-item-label>
                  <q-avatar>
                    <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
                  </q-avatar>
                  <div class="text-h6">qays</div>
                  <div class="text-body2">Employee ID: 23008</div>
                </q-item-label>
              </q-item-section>
            </q-item>

            <q-separator spaced />

            <q-item clickable v-ripple v-close-popup>
              <q-item-section side>
                <q-icon name="mdi-account-outline"></q-icon>
              </q-item-section>
              <q-item-section
                clickable
                @click="openInNewTab('http://10.10.120.32:3536/#/')"
              >
                <q-item-label> Manage account </q-item-label>
              </q-item-section>
            </q-item>

            <q-item @click="signOut()" clickable v-ripple v-close-popup>
              <q-item-section side>
                <q-icon name="mdi-logout"></q-icon>
              </q-item-section>
              <q-item-section>
                <q-item-label> Log Out </q-item-label>
              </q-item-section>
            </q-item>

            <q-item dense>
              <q-item-section>
                <q-item-label class="text-right">
                  Quasar v{{ $q.version }}
                </q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
      </q-toolbar>
    </q-header>

    <!-- <q-footer class="bg-grey-2">
      <q-toolbar class="footerCustomStyle">
        <q-toolbar-title class="text-black text-center text-caption">
          Copyright © 2022 PMD-MIS. All rights reserved.
        </q-toolbar-title>
      </q-toolbar>
    </q-footer> -->

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      :width="260"
      class="bg-grey-2"
      :mini="miniState"
      @mouseover="miniState = false"
      @mouseout="miniState = true"
      mini-to-overlay
      :breakpoint="100"
    >
      <q-list class="text-primary">
        <q-item
          active-class="my-menu-link"
          v-for="link in linksList"
          :key="link.title"
          clickable
          exact
          :to="link.path"
        >
          <q-item-section v-if="link.icon" avatar>
            <q-icon :name="link.icon" />
          </q-item-section>

          <q-item-section>
            <q-item-label>{{ link.title }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { useQuasar } from "quasar";
import { ref, getCurrentInstance, computed } from "vue";
const $q = useQuasar();
const app = getCurrentInstance().appContext.config.globalProperties;

const linksList = [
  {
    title: "Dashboard",
    icon: "dashboard",
    path: "/",
  },
  {
    title: "Graphs",
    icon: "query_stats",
    path: "/dashboard",
  },
  {
    title: "Customer",
    icon: "mdi-account-group-outline",
    path: "/customer",
  },
];

const leftDrawerOpen = ref(false);
const miniState = ref(true);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}

function openInNewTab(url) {
  window.open(url, "_blank").focus();
}
</script>

<style scoped>
.footerCustomStyle {
  min-height: 24px;
}

.my-menu-link {
  color: white;
  background: #1976d2;
  /* background: #26A69A; */
}

.mild-shadow {
  box-shadow: 0 2px 4px rgb(0 0 0 / 12%), 0 0 6px rgb(0 0 0 / 4%);
  transition: box-shadow 0.4s;
}
</style>
