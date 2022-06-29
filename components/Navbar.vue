<script setup lang="ts">
import Vue from 'vue'

export default Vue.extend({
    name: "Navbar",
    // async fetch(){
    //     // let id_menu_links = '';

    //     console.log(this.route);
    //     // if(this.route.path == '/') { id_menu_links = '1' }
    //     // if(this.route.path == '/route_1') { id_menu_links = '2' }

    //     // let get_links = 'http://localhost:3000/menuItems/'+id_menu_links;

    //     // let get_data = {};

    //     // get_data = await fetch(
    //     //     get_links
    //     // );

    //     // const newData = await fetch(
    //     //     get_links
    //     // ).then(res => res.json() )

    //     // console.log(newData);
    // },
    async fetch(){
        let id_menu_links = '';

        console.log(this.route);
        if(this.route.path == '/') { id_menu_links = '1' }
        if(this.route.path == '/route_1') { id_menu_links = '2' }

        let get_links = 'http://localhost:3000/menuItems/'+id_menu_links;

        // let get_data = {};

        // get_data = await fetch(
        //     get_links
        // );

        const newData = await fetch(
            get_links
        ).then(res => res.json() )

        console.log(newData);

        this.menuItems = newData.menuItems
    },
    fetchOnServer: false,
    data() {
        return {
            route: this.$route,
            menuItems: [
                {
                    link: '/',
                    name: 'menu 1'
                },
                {
                    link: '/route_1',
                    name: 'menu 2'
                },
                {
                    link: '/route_3',
                    name: 'menu 3'
                },
            ]
        };
    },
    methods: {
        
    },
    // watch: {
    //     $route(to, from) {
    //         console.log('route change to', to)
    //         console.log('route change from', from)
    //         this.fetchMenu()
    //     },
    // },
});
</script>

<template>
  <b-navbar toggleable="lg" type="dark" variant="dark">
    <!--Title NavBar-->
    <div>
        <div v-b-toggle.sidebarleft_cone>
            <img src="https://placekitten.com/g/30/30" class="d-inline-block align-top" alt="Kitten"></img>
        </div>
        <b-sidebar id="sidebarleft_cone" bg-variant="dark" text-variant="light" title="CiputraONE" width="200px">
            <div class="pt-1">
                <b-button block squared variant="dark" class="text-left" href="./">
                    <b-icon icon="house-fill" aria-hidden="true"></b-icon> 
                    &nbsp;Back To Home 
                </b-button>
            </div>

            <template v-for="item in menuItems">
                <b-button  block squared variant="dark" class="text-left my-0" v-bind:href="item.link" :active="item.link == route.fullPath">
                    &nbsp; {{item.name}}
                </b-button>
            </template>

        </b-sidebar>
    </div>
    &nbsp;
    &nbsp;
    <b-navbar-brand href="./" class="mr-10">
        <b>CiputraONE</b>
    </b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item href="#">Link</b-nav-item>
        <b-nav-item href="#" disabled>Disabled</b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-form>
          <b-form-input
            size="sm"
            class="mr-sm-2"
            placeholder="Search"
          ></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0" type="submit"
            >Search</b-button
          >
        </b-nav-form>

        <b-nav-item-dropdown text="Lang" right>
          <b-dropdown-item href="#">EN</b-dropdown-item>
          <b-dropdown-item href="#">ES</b-dropdown-item>
          <b-dropdown-item href="#">RU</b-dropdown-item>
          <b-dropdown-item href="#">FA</b-dropdown-item>
        </b-nav-item-dropdown>

        <b-nav-item-dropdown right>
          <!-- Using 'button-content' slot -->
          <template #button-content>
            <em>User</em>
          </template>
          <b-dropdown-item href="#">Profile</b-dropdown-item>
          <b-dropdown-item href="#">Sign Out</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>