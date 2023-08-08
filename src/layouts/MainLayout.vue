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

        <q-toolbar-title>
          My list
        </q-toolbar-title>

        <div>{{ dateToday }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item to="/" exact>
          <q-item-section avatar>
            <q-icon name="list" />
          </q-item-section>
          <q-item-section avatar>
            Todos
          </q-item-section>
        </q-item>


        <q-item to="/help">
          <q-item-section avatar>
            <q-icon name="help" />
          </q-item-section>
          <q-item-section avatar>
            Help
          </q-item-section>
        </q-item>


        <q-item to="/about">
          <q-item-section avatar>
            <q-icon name="link" />
          </q-item-section>
          <q-item-section avatar>
            About
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <div class="q-px-md">
        <router-view />
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref, computed } from 'vue'
import { date } from 'quasar'


export default defineComponent({
  name: 'MainLayout',

  setup () {
    const leftDrawerOpen = ref(false)
    const dateToday = computed( () => date.formatDate(Date.now(), 'dddd D MMMM'));

    return {
      dateToday,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
