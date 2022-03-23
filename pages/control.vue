<template>
    <div>
        <div class="alert alert-warning fixed-top text-center" role="alert" id="alerta1" style="display:none;left: 50%;transform: translateX(-50%); width: 30%; margin-top: 2rem;">
                    No se puede pasar de este valor
                </div>
                <div class="alert alert-warning fixed-top text-center" role="alert" id="alerta2" style="display:none;left: 50%;transform: translateX(-50%); width: 30%; margin-top: 2rem;">
                    Robot en posición no apta para esta carga
                </div>
            
                <div class="container-fluid px-sm-5 py-3 py-sm-0">
                    <div class="row g-5 my-sm-2">
                        <div class="col-md-10">
                            <div class="card p-sm-3 bg-secondary shadow-sm d-flex rounded card-artic">
                                <div>
                                    <p class="fs-6 px-3 pt-3 p-sm-0">Articulaciones</p>
                                </div>
                                <!--Inputs range-->
                                <!-- v-for recorre los valores de setpoints, index devuelve la posicion de la key del objeto:  -->
                                <div class="container mb-3 mb-sm-0">
                                    <div class="row" v-for=" (motor, index) in motores" :key="motor">
                                        <div class="col-md-2">
                                            <p class="text-center fw-bold">{{motor}}</p>
                                        </div>
                                    <!-- Articualcion 0, 2, 4, 5 -->
                                        <div v-if = "index == 0 || index == 2 || index ==  4 || index ==  5" class="col-md-10 d-flex justify-content-center">
                                            <input v-model="setpoints[index]" type="range" value="0" class="form-range slider" min="-90" max="90" oninput="this.nextElementSibling.value = this.value" onmouseup="this.nextElementSibling.value = this.value" onkeydown="return false;">
                                            <output class="text-end" style="margin-left: 1rem; min-width: 2rem;">{{setpoints[index].setpoint}}</output><span style="font-size: 1rem; margin-right: 1rem; margin-left: 0.5rem;">°</span>
                                        </div>     
                                    <!-- Articualcion1  -->
                                        <div v-else-if="index == 1"  class="col-md-10 d-flex justify-content-center">
                                            <input v-model="setpoints[index]" type="range" value="0" class="form-range slider" min="-80" max="80" oninput="this.nextElementSibling.value = this.value" onmouseup="this.nextElementSibling.value = this.value" onkeydown="return false;">
                                            <output class="text-end" style="margin-left: 1rem; min-width: 2rem;">{{setpoints[index].setpoint}}</output><span style="font-size: 1rem; margin-right: 1rem; margin-left: 0.5rem;">°</span>
                                        </div>     
                                 
                                            <div v-else  class="col-md-10 d-flex justify-content-center">
                                            <input v-model="setpoints[index]" type="range" value="0" class="form-range slider" min="-75" max="75" oninput="this.nextElementSibling.value = this.value" onmouseup="this.nextElementSibling.value = this.value" onkeydown="return false;">
                                            <output class="text-end" style="margin-left: 1rem; min-width: 2rem;">{{setpoints[index].setpoint}}</output><span style="font-size: 1rem; margin-right: 1rem; margin-left: 0.5rem;">°</span>
                                        </div>     
                                 
                                    </div> 
                                <!-- Botones de ejecutar -->
                                    <div class="row">
                                        <div class="col-md-2">
                                            <p class="text-center fw-bold">{{motor}}</p>
                                        </div>
                                        <div class="col-md-10 d-flex justify-content-end">
                                           <!-- Ejecutar -->
                                           <button @click="publish_sliders_value()" type="button" class="btn btn-secondary" value="" style="padding: 2vh; margin-right:1em; background: #488FB1; border-width: 0px">Ejecutar</button>
                                            <!-- Previzualizar -->
                                            <button type="button" class="btn btn-secondary" value="" style="padding: 1vh;">Previsualizar</button>
                                        </div>                    
                                                 
                                    </div>                            
                                </div>

                            </div>
                        </div>
                        <div class="col-md-2">
                            <!--Input velocidad-->
                            <div class="card p-3 bg-secondary shadow-sm d-flex justify-content-around align-items-center rounded card-vel">
                                <div class="name-vel">
                                    <p class="fs-6">Velocidad</p>
                                </div>
                                <div class="slider-wrapper d-flex justify-content-center">
                                    <input type="range" class="form-range" min="1" max="100" value="100" step="1" name="RangeV" id="RangeV" oninput="this.nextElementSibling.value = this.value" onmouseup="this.nextElementSibling.value = this.value" onkeydown="return false;">
                                    <output class="num-vel">100</output>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-2">
                            <!--Input Carga-->
                            <div class="card p-3 bg-secondary shadow-sm d-flex rounded" style="min-height: 13.79rem;">
                                <div class="text-center mb-3">
                                    <p class="fs-6">Carga</p>
                                </div>
                                <div class="text-center">
                                    <label class="pb-1" for="cargaMotores">lim: 0-2</label>
                                    <div class="d-flex justify-content-center px-3 pb-3">
                                        <input class="form-control text-center" type="number" min="0" max="2" placeholder="0" value="0" step="0.1" id="cargaMotores">
                                    </div>
                                    <label for="cargaMotores">Kg</label>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-3">
                            <!--Input Coordenadas-->
                            <div class="card p-3 bg-secondary shadow-sm d-flex rounded" style="min-height: 13.79rem;">
                                <div>
                                    <p class="fs-6 mb-3">Coordenadas</p>
                                </div>
                                <div class="row gy-4 px-3 justify-content-center">
                                    <div class="col-12 col-xl-10" style="text-align: center;">
                                        <div class="input-group input-group-sm">
                                            <span class="input-group-text">X</span>
                                            <input type="number" min="-360" max="360" step="0.1" class="form-control text-center" placeholder="" value="" id="coordenadaX">
                                            <span class="input-group-text">mm</span>
                                        </div>
                                    </div>
                                    <div class="col-12 col-xl-10" style="text-align: center;">
                                        <div class="input-group input-group-sm">
                                            <span class="input-group-text">X</span>
                                            <input type="number" min="-360" max="360" step="0.1" class="form-control text-center" placeholder="" value="" id="coordenadaX">
                                            <span class="input-group-text">mm</span>
                                        </div>
                                    </div>
                                    <div class="col-12 col-xl-10" style="text-align: center;">
                                        <div class="input-group input-group-sm">
                                            <span class="input-group-text">X</span>
                                            <input type="number" min="-360" max="360" step="0.1" class="form-control text-center" placeholder="" value="" id="coordenadaX">
                                            <span class="input-group-text">mm</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-7">
                            <!--Input botones-->
                            <div class="card p-3 pb-sm-2 bg-secondary shadow-sm d-flex rounded">
                                <div>
                                    <p class="fs-6 mb-2">Controles</p>
                                    <div class="container">
                                        <div class="row d-flex align-items-center" style="min-height: 10.17rem;">
                                            <div class="col-md-4">
                                                <div class="container">
                                                    <div class="d-flex flex-column"> 
                                                        <div class="d-flex justify-content-center mb-3">
                                                            <input type="image" src="arrow.svg" value="0" name="vUp" id="vUp" class="arrows-v1" draggable="false">
                                                        </div>
                                                        <div class="d-flex justify-content-center">
                                                            <input type="image" src="arrow.svg" value="1" name="vDown" id="vDown" class="arrows-v2" draggable="false">
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="position-relative mb-4 mb-md-0" style="height: 2rem;">
                                                    <span class="position-absolute bottom-0 start-50 translate-middle-x">Vertical</span>
                                                </div>
                                            </div>
                                            <div class="col-md-4">
                                                <div class="container">
                                                    <div class="row">
                                                        <div class="col-4 d-flex justify-content-center align-items-center">
                                                            <input type="image" src="arrow.svg" value="2" name="hLeft" id="hLeft" class="arrows-h1" draggable="false">
                                                        </div>
                                                        <div class="col-4 d-flex justify-content-center">
                                                            <div class="d-flex flex-column"> 
                                                                <div class="d-flex justify-content-center mb-3">
                                                                    <input type="image" src="arrow.svg" value="3" name="hForward" id="hForward" class="arrows-h2" draggable="false">
                                                                </div>
                                                                <div class="d-flex justify-content-center">
                                                                    <input type="image" src="arrow.svg" value="4" name="hBackward" id="hBackward" class="arrows-h3" draggable="false">
                                                                </div>
                                                            </div>
                                                        </div>
                                                        <div class="col-4 d-flex justify-content-center align-items-center">
                                                            <input type="image" src="arrow.svg" value="5" name="hRight" id="hRight" class="arrows-h4" draggable="false">
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="position-relative" style="height: 2rem;">
                                                    <span class="position-absolute bottom-0 start-50 translate-middle-x">Horizontal</span>
                                                </div>
                                            </div>
                                            <div class="col-md-4">
                                                <div class="container">
                                                    <div class="row alineacion-v-rotacion">
                                                        <div class="col-6 d-flex justify-content-end">
                                                            <input type="image" src="arrow.svg" value="6" name="rLeft" id="rLeft" class="arrows-r1" draggable="false">
                                                        </div>
                                                        <div class="col-6 d-flex justify-content-start">
                                                            <input type="image" src="arrow.svg" value="7" name="rRight" id="rRight" class="arrows-r2" draggable="false">
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="position-relative" style="height: 4rem;">
                                                    <span class="position-absolute bottom-0 start-50 translate-middle-x">Rotación</span>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            

    </div>
</template>

<script>
export default {

     mounted(){
        var ros = new ROSLIB.Ros({
             url: "ws:/localhost:9090"
         })

         ros.on('connection', ()=>{
             console.log("Connected to websocket")
         })

         ros.on('error', (error) => {
             console.log('Error connecting: ', error)
         })

         ros.on('close', ()=>{
             console.log("Se cerro la conexion")
         })
            
      }, 

    data(){
        return{
            motores: ["motor 0", "motor 1", "motor 2", "motor 3", "motor 4", "motor 5"],
            setpoints: [
                {setpoint: 0}, 
                {setpoint: 0},
                {setpoint: 0},
                {setpoint: 0},
                {setpoint: 0},
                {setpoint: 0},
            ],

            ros: new ROSLIB.Ros({
             url: "ws:/localhost:9090"
            })
        }
    },

     methods: {
        // Envio de los setpoints de los sliders
        publish_sliders_value(){
            var sliders_value = new ROSLIB.Topic({
            ros: this.ros, 
            name: '/sliders_value',
            messageType: 'geometry_msgs/Twist'
            });

            var setpoints = new ROSLIB.Message({
                data: JSON.stringify(this.setpoints)   
            })
            
           sliders_value.publish(setpoints)


           console.log(this.setpoints)
        },



        
    }
    
}
</script>