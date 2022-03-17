<template>
        <!-- SideBar -->
        <div class="bg-dark" id="sidebar-wrapper">
                    <img src="logo.png" class="logo px-3">
                    <div class="list-group list-group-flush my-3">
                        <a class="list-group-item none"></a>
                        <Nuxt-link to="/control" class="list-group-item list-group-item-action fw-bold">
                            <span>Control</span>
                        </nuxt-link> 
                        <nuxt-link to="/ejecutar" class="list-group-item list-group-item-action fw-bold">
                            <span>Ejecutar</span>
                        </nuxt-link>
                        <nuxt-link to="/crear" class="list-group-item list-group-item-action fw-bold">
                            <span>Crear</span>
                        </nuxt-link>
                        <a class="list-group-item none"></a>
                    </div>
         </div>   
</template>