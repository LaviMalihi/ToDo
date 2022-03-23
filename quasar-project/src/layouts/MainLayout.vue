<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3"> מטלות</div>
        <div class="text-subtitle1">{{ todayDate }}</div>
        <div class="text-subtitle1"> פרשת השבוע : {{ pharasha }}</div>
      </div>
      <q-img class="header-image absolute-top"
             src="https://media.istockphoto.com/photos/amazing-sunrise-view-from-mountains-sun-sets-behind-the-mountain-view-picture-id1159495128?b=1&k=20&m=1159495128&s=170667a&w=0&h=Zs55RxCeQYtDUaYbOufTjwGrKnXPZy_K8u_mkp02lD4="/>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="280"
      :breakpoint="400"
    >
      <q-scroll-area style="height: calc(100% - 150px); margin-top: 150px; border-right: 1px solid #ddd">
        <q-list padding>
          <q-item clickable v-ripple>
          </q-item>

          <q-item to="/" exact active clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list"/>
            </q-item-section>

            <q-item-section>
              To do
            </q-item-section>
          </q-item>

          <q-item to="/help" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help"/>
            </q-item-section>

            <q-item-section>
              help
            </q-item-section>
          </q-item>

        </q-list>
      </q-scroll-area>

      <q-img class="side absolute-top"
             src="https://media.istockphoto.com/photos/amazing-sunrise-view-from-mountains-sun-sets-behind-the-mountain-view-picture-id1159495128?b=1&k=20&m=1159495128&s=170667a&w=0&h=Zs55RxCeQYtDUaYbOufTjwGrKnXPZy_K8u_mkp02lD4="
             style="height: 206.75px">
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://cdn.quasar.dev/img/boy-avatar.png">
          </q-avatar>
          <div></div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view/>
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import {date} from 'quasar'
import EssentialLink from 'components/EssentialLink.vue'
import Hebcal from 'hebcal';


export default {
  name: 'MainLayout',
  components: {
    EssentialLink
  },
  data() {
    return {
      leftDrawerOpen: false,
    }
  },
  computed: {
    todayDate() {
      const timeStamp = Date.now()
      let a = date.formatDate(timeStamp, 'dddd D MMMM')
      return new Hebcal.HDate();
    },
    pharasha() {
      let a = new Hebcal.HDate().getSedra('h')
      return a.toString()
    }
  }
}
</script>
<style lang="css">
.header-image {
  height: 100%;
  z-index: -3;
  /*opacity: 0.5;*/
  /*filter: grayscale(100%);*/
}

.side {
}
</style>
