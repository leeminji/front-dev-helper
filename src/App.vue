<template>
  <v-app>
    <!-- 왼쪽메뉴 -->
    <v-navigation-drawer
      v-model="drawer"
      fixed
      app
    >
      <v-toolbar color="purple darken-3" dark>
        <v-toolbar-title>MENU</v-toolbar-title>
      </v-toolbar>       
      <v-list dense>

        <v-list-tile @click="gotoRouter('/')">
          <v-list-tile-action>
            <v-icon>fas fa-home</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>메인으로</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
 
        <v-list-tile @click="gotoRouter('/mkList')">
          <v-list-tile-action>
            <v-icon>fas fa-code</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>태그 리스트만들기</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>

        <v-list-tile @click="gotoRouter('/mkText')">
          <v-list-tile-action>
            <v-icon>fas fa-font</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>텍스트변경(소문자/대문자)</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>

        <v-list-tile @click="gotoRouter('/about')">
          <v-list-tile-action>
            <v-icon>fas fa-sign-out-alt</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>로그아웃</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <!-- //왼쪽메뉴 -->
    <!-- 툴바 -->
    <v-toolbar
      color="purple"
      dark
      fixed
      app
      clipped-right
    >
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title>프론트 개발 HELPER V1</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon @click.stop="drawerRight = !drawerRight">
      <v-icon>more_vert</v-icon>
      </v-btn>
    </v-toolbar>
    <!-- //툴바 -->
    <!-- 오른쪽설정 -->
    <v-navigation-drawer
      v-model="drawerRight"
      fixed
      right
      app
    >
      <v-toolbar color="purple darken-3" dark>
        <v-toolbar-title>설정</v-toolbar-title>
      </v-toolbar>    
      <v-list subheader two-line>
        <v-list-tile @click.stop="right = !right">
          <v-list-tile-title>Notifications</v-list-tile-title>
          <v-list-tile-sub-title>Allow notifications</v-list-tile-sub-title>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <!-- //오른쪽설정 -->
    <v-content>
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data: () => ({
    drawer: null,
    drawerRight: null
  }),
  props: {
    source: String
  },
  methods : {
    gotoRouter(_path){
      this.$router.push({ path: _path });
    },
  }
}
</script>
