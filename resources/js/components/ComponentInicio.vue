<template>
<!-- App.vue -->

<v-app>
    <v-container fluid>
        <v-toolbar>
          <v-app-bar-nav-icon @click="drawer =!drawer"></v-app-bar-nav-icon>
          <v-toolbar-title>Sistema de control de asistencia</v-toolbar-title>
          <v-spacer></v-spacer>
            <v-menu bottom left 
       v-model="value"
      :disabled="disabled"
      :absolute="absolute"
      :open-on-hover="openOnHover"
      :close-on-click="closeOnClick"
      :close-on-content-click="closeOnContentClick"
      :offset-x="offsetX"
      :offset-y="offsetY"           
            >
            <template v-slot:activator="{ on }">
              <v-btn
                dark
                icon
                v-on="on"
                color="blue"
              >
                <v-icon>fas fa-id-badge</v-icon>
              </v-btn>
            </template>

            <v-list >
                <v-list-item @click="prueba">
                <v-list-item-title>Mi Perfil </v-list-item-title>
              </v-list-item>              
              <v-list-item @click="cerrar">
                <v-list-item-title>Cerrar Sesion
                </v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>  
        </v-toolbar>
<!--Navegation -->

      <!--<v-navigation-drawer v-model="drawer" absolute temporary dark row>
        <v-layout column mt-4>
          <v-flex>
              <v-avatar>
                <img src="/imagenes/logo.png" alt="">
              </v-avatar>
              <h3>I.E. Jose Maria Arguedas</h3>
          </v-flex>
          <v-flex>
            <v-btn color="primary" :to="{name: 'home'}" text>
              Inicio
            </v-btn>
            <v-btn color="primary" :to="{name: 'persona'}" text>
              Persona
            </v-btn>
          </v-flex>

        </v-layout>

      </v-navigation-drawer>-->
    <v-navigation-drawer
      :width="width"
      v-model="drawer"
      
      absolute
      temporary
    >
      <v-img :aspect-ratio="16/9" src="https://cdn.vuetifyjs.com/images/parallax/material.jpg">
        <v-row align="end" class="lightbox white--text pa-2 fill-height">
          <v-col>
            <div class="subheading">Jonathan Lee</div>
            <div class="body-1">heyfromjonathan@gmail.com</div>
          </v-col>
        </v-row>
      </v-img>

      <v-list>
        <template >
          <v-divider ></v-divider>
          <v-list-item >
            <v-list-item-action>
              <v-icon>fas fa-home</v-icon>
            </v-list-item-action>
            <v-list-item-action>
              <v-list-item-title> Inicio</v-list-item-title>
            </v-list-item-action>
          </v-list-item>
          <v-list-item >
            <v-list-item-action>
              <v-icon>fas fa-users</v-icon>
            </v-list-item-action>
            <v-list-item-action>
              <v-list-item-title > <router-link to="/persona">Persona </router-link> </v-list-item-title>
            </v-list-item-action>
          </v-list-item>
        </template>
      </v-list>
    </v-navigation-drawer>
<!-- Fin de navegacion -->
      <v-layout>
        <v-content>
          <router-view>

          </router-view>
        </v-content>
      </v-layout>
    </v-container>
</v-app>

</template>

<script>
    
    export default {
      data(){
        return{
          drawer:false,
          disabled: false,
          absolute: false,
          openOnHover: false,
          value: false,
          closeOnClick: true,
          closeOnContentClick: true,
          offsetX: false,
          offsetY: true,
          csrf:'',
          width: 300
        }
      },
      methods: {
        prueba(){
          alert('Mi perfil')
        },
        cerrar(){
          var token=$('meta[name="csrf-token"]').attr('content')
          axios.post('logout',token).then(()=>{
            localStorage.removeItem('auth_token');
            location.reload();
          })
        }
      }
    }
</script>
