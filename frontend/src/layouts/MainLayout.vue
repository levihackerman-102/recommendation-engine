<template>
  <q-layout view="hhh lpR fFf">

    <q-header reveal elevated class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn-icons-png.flaticon.com/512/3418/3418886.png">
          </q-avatar>
          Movie Recommendation Engine
        </q-toolbar-title>
      </q-toolbar>

      <q-tabs align="left">
        <q-route-tab to="/" label="Home" />
        <q-route-tab to="/about" label="About" />
      </q-tabs>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer elevated class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <p class="footerText"> Made with <q-icon name="favorite" color="red"/> by <a href="https://github.com/levihackerman-102/" target=”_blank” class="footerLink">Anshul Singh</a></p>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<style>
  .footerLink {
    color: aquamarine;
  }
  .footerLink:hover {
    color: antiquewhite;
  }
  .footerText {
    margin-bottom: 0.1rem;
  }
</style>
