// Este estilo se aplica para todo el documento 
<template>
  <div class="d-flex" id="wrapper" style="background-color: #0d161d;">
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
        },
        {
          src: "http://static.robotwebtools.org/EventEmitter2/current/eventemitter2.min.js"
        },
        {
         src: "http://static.robotwebtools.org/roslibjs/current/roslib.min.js" 
        }
      ]
    }
  },
}
</script>