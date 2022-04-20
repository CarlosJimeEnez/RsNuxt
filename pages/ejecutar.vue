<template>
    <div class="container-fluid px-sm-5 py-3 py-sm-0">
                    <div class="row g-5 my-sm-2">
                        <div class="col-md-12">
                            <div class="card p-sm-3 bg-secondary shadow-sm d-flex rounded" style="min-height: 78.5vh;">
                                <div class="container" style="margin-top: 1.4rem;">
                                    <div class="row">
                                        <div class="col-md-6">
                                            <div class="row mb-4">
                                                <div class="col-12">
                                                    <div class="mb-4" style="max-width: 82%;">
                                                        <label for="formFile" class="form-label mb-3 fs-5">Importar archivo</label>
                                                        <!-- Importamos el archivo -->
                                                        <input @change="cambiar_disp_btn" class="form-control form-control-sm" type="file" id="formFile" accept=".json">
                                                    </div>
                                                </div>
                                                <div class="col-3 d-grid mb-3">
                                                    <button type="button" value="0" name="" id="btnLeer" class="btn btn-secondary p-1" @click="Leer_valores()" disabled >
                                                        <span>Leer</span>
                                                    </button>
                                                </div>
                                                <div class="col-3 d-grid mb-3">
                                                    <button @click="ejecutar()" type="button" value="0" name="" id="btnEjecutar" class="btn btn-secondary p-1" disabled>
                                                        <span>Ejecutar</span>
                                                    </button>
                                                </div>
                                            </div>
                                            <div class="row mb-4">
                                                <div class="col-12">
                                                    <div class="mb-3" style="max-width: 82%;">
                                                        <span class="form-label mb-3 fs-5">Entrada ejecución 01</span>
                                                    </div>
                                                </div>
                                                <div class="col-3 d-grid mb-3">
                                                    <button type="button" value="0" name="" id="btnIniciar" class="btn btn-secondary p-1" disabled>
                                                        <span>Iniciar</span>
                                                    </button>
                                                </div>
                                                <div class="col-3 d-grid mb-3">
                                                    <button type="button" value="0" name="" id="btnParar" class="btn btn-secondary p-1" disabled>
                                                        <span>Parar</span>
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="col-md-6 float-end">
                                            <!-- Mostramos el texto -->
                                            <textarea class="form-control align-top mb-3" type="text" id="txtInfo" readonly style="height: 45vh; background-color:#ced4da; resize: none;"></textarea>
                                            <div class="row justify-content-end">
                                                <div class="col-auto mb-3">
                                                    <nuxt-link to="/crear">
                                                        <button @click="mostrar_bloques()" type="button" value="0" name="" id="btnBloques" class="btn btn-secondary p-1" disabled>
                                                        <span>Abrir en bloques</span>
                                                        </button>
                                                    </nuxt-link>
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

    data (){
        return {
            input: 0,
            listOfBlocks: "", //-> Variable donde guardamos el contenido del json que cargamos del archivo
            listaDeBloques: [], //-> Lista con todas las ordenes de movimiento, guardadas de forma ordenada.
            localizacionArchivo: "", // -> Localizacion en el disco de el archivo. 
            //Ros
            ros: new ROSLIB.Ros({
                url: "ws:/localhost:9090"
            })
        }
    }, 

    methods: {
        cambiar_disp_btn(){
            $( "#btnLeer" ).prop( "disabled", false);
            $("#btnBloques").prop("disabled", true)
            $("#btnParar").prop("disabled", true)
            $("#btnIniciar").prop("disabled", true)
            $("#btnEjecutar").prop("disabled", true)
            let empty_str = ''
            $("#txtInfo").val(empty_str)
        }, 

        Leer_valores(){ 
            $("#btnBloques").prop("disabled", false)
            $("#btnParar").prop("disabled", false)
            $("#btnIniciar").prop("disabled", false)
            $("#btnEjecutar").prop("disabled", false)

            // Tomamos el nombre del archivo que se cargo en el input y buscamos en la carpeta por ese nombre:
            let input = document.getElementById("formFile")
            console.log(input.files[0].name)
            let name = input.files[0].name 
            //Guardamos en la variable un json con los movimientos: 
            this.localizacionArchivo = '/home/bleary/pruebas/' + name
            this.listOfBlocks = require('/home/bleary/pruebas/' + name)
            console.log(this.listOfBlocks)
            console.log(this.listOfBlocks.length)
            var str = ""
            for(var i = 0; i < this.listOfBlocks.length; i++){
                //COORDENADA: 
                if (this.listOfBlocks[i].tipo == "coordenada"){
                    str = i + " - Tipo:" + this.listOfBlocks[i].tipo + "\n  Velocidad: " + this.listOfBlocks[i].velocidad + ", Delay: " + this.listOfBlocks[i].delay  + 
                    ", coordenadas: [ x: " + this.listOfBlocks[i].paths[0] + ", y: " + this.listOfBlocks[i].paths[1] + ", z: " + this.listOfBlocks[i].paths[2] + " ]\n\n"    
                    this.listaDeBloques.push(str)
                }
                //GRADO
                else if (this.listOfBlocks[i].tipo == "grado"){
                    str = i + " - Tipo: " + this.listOfBlocks[i].tipo + "\n Grados: [ M0: " + 
                    this.listOfBlocks[i].angulos[0] +
                    ", M1: " + this.listOfBlocks[i].angulos[1] + 
                    ", M2: " + this.listOfBlocks[i].angulos[2] + 
                    ", M3: " + this.listOfBlocks[i].angulos[3] + 
                    ", M4: " + this.listOfBlocks[i].angulos[4] +
                    ", M5: " + this.listOfBlocks[i].angulos[5] + "] \n" + 
                    " Velocidad: " + this.listOfBlocks[i].velocidad + 
                    " Delay: " + this.listOfBlocks[i].delay + "\n\n"
                    console.log(this.listOfBlocks[i].angulos[3])

                    this.listaDeBloques.push(str)
                }
                //SALIDA
                else if (this.listOfBlocks[i].tipo == "salida"){
                    str = i + " - Tipo: " + this.listOfBlocks[i].tipo + "\n " + 
                    "Salidas: [ Sal0: " +  
                    this.listOfBlocks[i].salidas[0] + 
                    ", Sal1: " + this.listOfBlocks[i].salidas[1] + 
                    ", Sal2: " + this.listOfBlocks[i].salidas[2] +
                    ", Sal3: " + this.listOfBlocks[i].salidas[3] + 
                    ", Sal4: " + this.listOfBlocks[i].salidas[4] + "] \n" +
                    " delay: " + this.listOfBlocks[i].delay + "\n\n"
                    this.listaDeBloques.push(str) 
                }
                //ENTRADA
                else if (this.listOfBlocks[i].tipo == "entrada"){
                    str = i + " - Tipo: " + this.listOfBlocks[i].tipo + "\n " + 
                    "Entrada selec: " + this.listOfBlocks[i].entrada_select + 
                    "\n Continuar en: " + this.listOfBlocks[i].continuar_en +
                    "\n Valor de entrada: " + this.listOfBlocks[i].valor_entrada + 
                    "\n delay: " + this.listOfBlocks[i].delay +
                    "\n\n"
                    this.listaDeBloques.push(str)
                }
                //GRIPPER
                else if (this.listOfBlocks[i].tipo == "gripper"){
                    str = i + " - Tipo: " + this.listOfBlocks[i].tipo + "\n " + 
                    "Apertura: " + this.listOfBlocks[i].apertura + 
                    "\n Delay: " + this.listOfBlocks[i].delay + 
                    "\n\n"
                    this.listaDeBloques.push(str)
                }
            }
            $("#txtInfo").val(this.listaDeBloques)
            $("#btnLeer").prop("disabled", true)
        },
        
        ejecutar(){ 
            //Ejecuta las ordenes del archivo cargado: 
            var ejecutar = new ROSLIB.Topic({
                ros: this.ros, 
                name: '/ejecutar_archivo',
                messageType: 'std_msgs/String'
            });
            var localizacion = new ROSLIB.Message({
            data: JSON.stringify(this.localizacionArchivo)   
            })
            ejecutar.publish(localizacion)  
            console.log(this.localizacionArchivo)      
        }, 

        mostrar_bloques(){
            localStorage.setItem("Lista_movimientos", JSON.stringify(this.listOfBlocks))
        }
    }

}
</script>