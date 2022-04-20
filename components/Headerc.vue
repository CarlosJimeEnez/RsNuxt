<template>
  <nav class="navbar navbar-expand-lg bg-dark py-4 px-4">
    <div class="d-flex align-items-center">
      <img src="toggle.svg" @click="menu_toggle()" id="menu-toggle" />
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return{

    }
  }, 

  methods: {
    menu_toggle(){
      alert("asd")
    }
  }
}
</script>