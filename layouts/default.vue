<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      clipped
      app
      fixed
      height="100%"
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar clipped-left fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? "right" : "left"}` }}</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-cog</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container style="margin-bottom: 100px">
        <nuxt />
      </v-container>
      <FlashMessage style="position: fixed; z-index: 10;"></FlashMessage>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon> mdi-repeat </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer</v-list-item-title>
        </v-list-item>
        <v-divider></v-divider>
        <v-list-item>
          <v-icon left>mdi-theme-light-dark</v-icon>
          <v-list-item-title>Theme Dark</v-list-item-title>
          <v-list-item-action>
            <v-switch v-model="$vuetify.theme.dark" inset></v-switch>
          </v-list-item-action>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer app padless inset :absolute="!fixed" outlined>
      <v-card width="100%" class="text-center" flat tile>
        <v-divider></v-divider>
        <v-card-text>
          {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
        </v-card-text>
      </v-card>
    </v-footer>
    <v-btn v-scroll="onScroll" v-show="fab" fab fixed bottom right color="primary" @click="toTop">
      <v-icon>mdi-chevron-up</v-icon>
    </v-btn>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: true,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Thông tin chung",
          to: "/",
        },
        {
          icon: "mdi-shape",
          title: "Các mô hình nổi bật",
          to: "/models",
        },
        {
          icon: "mdi-fast-forward",
          title: "Phân đoạn ảnh Polyb",
          to: "/predict",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Phân đoạn Polyp",
      iconsFooter: ["mdi-facebook", "mdi-twitter", "mdi-linkedin", "mdi-instagram"],
      fab: false
    };
  },
  methods: {
    onScroll(e) {
      if (typeof window === 'undefined') return
      const top = window.pageYOffset || e.target.scrollTop || 0
      this.fab = top > 20
    },
    toTop() {
      this.$vuetify.goTo(0)
    }
  }
};
</script>
