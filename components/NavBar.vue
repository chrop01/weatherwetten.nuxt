<template>
  <v-app>

    <v-app-bar app color="black">
      <v-toolbar color="black">
        <v-app-bar-nav-icon color="white" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
        <div class="pb-2">
          <v-img
            max-height="60"
            max-width="60"
            :src="require('../assets/img/icon.png')"></v-img>
        </div>
        <v-toolbar-title>WEATHER WETTEN</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items class="hidden-sm-and-down">
          <v-btn color="black">
            <nuxt-link to="/profile" tag="a">PROFILE</nuxt-link>
          </v-btn>
          <v-btn color="black">
            <nuxt-link to="/bet" tag="a">BET</nuxt-link>
          </v-btn>
          <v-btn color="black">
            <nuxt-link to="/leaderboards" tag="a">LEADERBOARDS</nuxt-link>
          </v-btn>
          <v-btn color="black">
            <nuxt-link to="/weathercoin" tag="a">WEATHERCOIN</nuxt-link>
          </v-btn>
          <v-btn color="black">
            <nuxt-link to="/aboutus" tag="a">ABOUT US</nuxt-link>
          </v-btn>
        </v-toolbar-items>
      </v-toolbar>
    </v-app-bar>

    <!-- NAVBAR DRAWER -->
    <v-navigation-drawer
      v-model="drawer"
      absolute
      temporary
      color="black"
    >

      <v-list dense>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>
              <nuxt-link :to="{ path: item.link, query: { plan: 'private' }}">{{ item.title }}</nuxt-link>
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main color="white">

      <span class="hero"></span>
      <!-- Overlay over img-->
      <v-overlay absolute>
        <v-card flat color="transparent" >
          <v-card-text class="white--text font-weight-black text-center d-flex flex-column align-center justify-center"
            :class="headingClass">BET WITH WEATHERCOIN</v-card-text>
          <v-card-subtitle class="white--text text-center d-flex flex-column align-center justify-center" :class="subtitleClass">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aperiam autem blanditiis, commodi cum dignissimos dolor dolore enim eum id illum in iusto, nemo omnis placeat, quis quisquam<br> sed sequi veritatis. Minima, quibusdam, quos! Consectetur ducimus eaque et, fuga iure labore maiores modi <br>possimus praesentium quas quisquam quod quos ratione, reiciendis!</v-card-subtitle>
        </v-card>
      </v-overlay>

      <!-- <iframe
        width="560"
        height="315"
        :src="require('../assets/img/video.mp4')"
        frameborder="0"
        allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      ></iframe> -->
    </v-main>

    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null,
      items: [
        {title: 'PROFILE', icon: 'mdi-view-dashboard', link: 'profile'},
        {title: 'BET', icon: 'mdi-view-dashboard', link: 'bet'},
        {title: 'LEADERBOARD', icon: 'mdi-view-dashboard', link: 'leaderboards'},
        {title: 'WEATHERCOIN', icon: 'mdi-view-dashboard', link: 'weathercoin'},
        {title: 'ABOUT US', icon: 'mdi-view-dashboard', link: 'aboutus'},
      ],
    }
  }
}

</script>

<style>
.hero {
  background: url('../assets/img/hero.jpg');
  background-size: cover;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  transform: scale(1.03); /*to scale img right to main element (not really a good way but working)*/
}
.overlay{
  justify-content: center;
  align-items: center;
  transform: scale(1.03);
}
</style>
