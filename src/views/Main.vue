<template>
  <v-app>
    <v-app-bar app :color="bg" flat>
      <div v-if="$vuetify.breakpoint.mdAndUp" class="d-flex align-center">
        <v-img
          alt="MOSQU Logo"
          class="shrink mr-2"
          contain
          :src="require('@/assets/mosqu-logo.png')"
          width="50"
        />
        <div class="menu ml-10">
          <a href="/#home" style="text-decoration: none;">
            <v-btn text :ripple="true" exact>Beranda</v-btn>
          </a>
          <a href="/#about" style="text-decoration: none;">
            <v-btn text :ripple="true" >Tentang</v-btn>
          </a>
          <a href="/#feature" style="text-decoration: none;">
            <v-btn text :ripple="true">Fitur</v-btn>
          </a>
          <a href="/#faq" style="text-decoration: none;">
            <v-btn text :ripple="true">FAQ</v-btn>
          </a>
          <v-btn text :ripple="true" to="/cari/masjid">Cari Masjid</v-btn>
          <v-btn text :ripple="true" to="/cari/program">Cari Program</v-btn>
        </div>
      </div>

      <v-app-bar-nav-icon
        v-else
        @click.stop="drawer = !drawer"
      />

      <v-flex v-if="$vuetify.breakpoint.smAndDown" class="d-flex" align-center>
        <v-img
          alt="MosQu Logo"
          class="mr-2 shrink align-self-center"
          contain
          :src="require('@/assets/mosqu-logo.png')"
          width="50"
        />
        <h3>MosQu</h3>
      </v-flex>

      <v-spacer></v-spacer>

      <a href="https://bit.ly/PendaftaranMosqu" style="text-decoration: none;">
        <v-card
          class="px-4 text-button"
          v-if="!this.$store.getters.isLoggedIn && $vuetify.breakpoint.smAndUp"
          color="teal white--text"
          :ripple="true"
          style="text-decoration: none; background-color: inherit"
          elevation="0"
          >DAFTAR</v-card
        >
      </a>
      <v-card
        flat
        class="px-4 text-button"
        v-if="!this.$store.getters.isLoggedIn && $vuetify.breakpoint.smAndUp"
        text
        color="grey--text text--darken-2"
        :ripple="true"
        style="text-decoration: none; background-color: inherit"
        to="/masuk"
        >MASUK</v-card
      >

      <div v-if="this.$store.getters.isLoggedIn">
        Selamat datang,
        <span style="font-weight: bold">
          {{ this.$store.getters.getUser }}
        </span>
        <v-btn text color="secondary" :ripple="true" to="/admin">Admin</v-btn>
        <v-icon @click="logout">mdi-logout</v-icon>
      </div>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" fixed temporary>
      <v-flex class="ma-2 d-flex" align-center>
        <v-img
          alt="MosQu Logo"
          class="mr-2 shrink align-self-center"
          contain
          :src="require('@/assets/mosqu-logo.png')"
          width="50"
        />MosQu
      </v-flex>
      <v-list nav>
        <v-list-item-group>
          <v-list-item exact>
            <a href="/#home" class="black--text" style="text-decoration: none;">Beranda</a>
          </v-list-item>

          <v-list-item>
            <a href="/#about" class="black--text" style="text-decoration: none;">About</a>
          </v-list-item>

          <v-list-item>
            <a href="/#feature" class="black--text" style="text-decoration: none;">Fitur</a>
          </v-list-item>

          <v-list-item>
            <a href="/#faq" class="black--text" style="text-decoration: none;">FAQ</a>
          </v-list-item>

          <v-list-item to="/cari/masjid">Cari Masjid</v-list-item>

          <v-list-item to="/cari/program">Cari program</v-list-item>

          <v-list-item to="/#daftar">
            <a href="https://bit.ly/PendaftaranMosqu" class="black--text" style="text-decoration: none;">Daftar</a>
          </v-list-item>

          <v-list-item to="/masuk">Masuk</v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
  
  export default {
    data() {
      return {
        drawer: false,
        bg: 'white'
      };
    },
    methods: {
      isHome: function () {
        return this.$route.path.includes("home");
      },
      logout: function () {
        this.$store.dispatch("logout");
      },
      changeColor() {
        if (
          document.body.scrollTop > 100 ||
          document.documentElement.scrollTop > 100
        ) {
          this.bg = 'white';
        } else {
          this.bg = 'white';
        }
      },
    },
    mounted() {
      window.onscroll = () => {
        this.changeColor();
      };
    },
  
  };
</script>