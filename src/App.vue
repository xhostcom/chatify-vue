<template>
  <v-app>
    <v-navigation-drawer absolute temporary v-model="drawerToggle">
      <v-list>
        <v-list-item>
          <v-list-item-action>
            <v-icon>mdi-account</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            Online Users {{onlineUsers[0]}}
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-list >
        <v-list-item avatar v-for="user in onlineUsers[1]" v-bind:key="user.user.username">
          <v-list-item-avatar>
            <img src="https://randomuser.me/api/portraits/men/85.jpg" />
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title>{{user.user.username}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar app class="light-blue darken-1">
      <v-app-bar-nav-icon @click.native.stop="drawerToggle = !drawerToggle"></v-app-bar-nav-icon>
      <v-toolbar-title>
        <router-link to="/chat/0" tag="span" style="cursor: pointer">Chatify Vue</router-link>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items v-for="item in menuItems" v-bind:key="item.route">
        <v-btn text :key="item.title" :to="item.route">
          <v-icon left>{{ item.icon }}</v-icon>
          <div class="hidden-xs-only">{{ item.title }}</div>
        </v-btn>
      </v-toolbar-items>
    </v-app-bar>
    <v-content>
      <router-view></router-view>
    </v-content>
  <Footer />
  </v-app>
</template>

<script>
 import Footer from './components/Footer.vue'
  export default {
    data () {
      return {
        drawerToggle: false
      }
    },
    components: {
      Footer
    },
    computed: {
      menuItems () {
        let items = [
          { icon: 'mdi-face', title: 'Register', route: '/register' },
          { icon: 'mdi-lock-open', title: 'Login', route: '/login' }
        ]
        if (this.userIsAuthenticated) {
          items = [
            {icon: 'mdi-forum', title: 'Create a Chat', route: '/create'},
            {icon: "mdi-chat", title: 'Chat List', route: '/discover'}
          ]
        }
        return items
      },
      userIsAuthenticated () {
        return this.$store.getters.user !== null && this.$store.getters.user !== undefined
      },
      onlineUsers () {
        return this.$store.getters.onlineUsers
      }
    }
  }
</script>

<style>
#app > div > header > div > div.v-toolbar__title > span {
  color:aliceblue;
}
</style>
