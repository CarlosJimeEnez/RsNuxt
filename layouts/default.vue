<template>
  <div class="d-flex" id="wrapper">
    <SideBar />
    <div id="page-content-wrapper">
        <Headerc />
        <Nuxt />
    </div>
  </div>
</template>


<script>
export default {
  head(){
    return {
      link: [
        {
          rel: 'stylesheet',
          href: 'css/bootstrap.min.css', 
        },
        {
          rel: 'stylesheet',
          href: 'css/style.css'
        }
      ], 
      script: [
        {
          src: 'js/bootstrap.bundle.min.js', 
        }, 
        {
          src: 'js/bootstrap.min.js',
        },
        {
          src: 'js/jquery.js',
        }
      ]
    }
  }
}
</script>