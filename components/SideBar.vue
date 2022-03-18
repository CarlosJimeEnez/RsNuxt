<template>
        <!-- SideBar -->
        <div class="bg-dark" id="sidebar-wrapper">
                    <img src="logo.png" class="logo px-3">
                    <div class="list-group list-group-flush my-3">
                        <a class="list-group-item none"></a>
                        <Nuxt-link to="/control" class="list-group-item list-group-item-action fw-bold">
                            <span>Control</span>
                        </Nuxt-link> 
                        <Nuxt-link to="/crear" class="list-group-item list-group-item-action fw-bold">
                            <span>Crear</span>
                        </Nuxt-link>
                        <Nuxt-link to="/ejecutar" class="list-group-item list-group-item-action fw-bold">
                            <span>Ejecutar</span>
                        </Nuxt-link>
                        <a class="list-group-item none"></a>
                    </div>
         </div>   
</template>