<template>
  <div>
    <div
      class="alert alert-danger fixed-top text-center"
      role="alert"
      id="alerta1"
      style="
        display: none;
        left: 50%;
        transform: translateX(-50%);
        width: 30%;
        margin-top: 2rem;
      "
    >
      Es necesario introducir un nombre
    </div>
    <div class="container-fluid px-sm-5 py-3 py-sm-0">
      <div class="row g-5 my-sm-2">
        <div class="col-md-12">
          <div
            class="card p-sm-3 bg-secondary shadow-sm d-flex rounded"
            style="min-height: 78.5vh"
          >
            <div class="container" id="bloquesCrear" style="margin-top: 1.4rem">
              <div class="row">
                <div class="col-md-12 mb-4">
                  
                    <div
                      class="row rss justify-content-end mx-1 sticky-top"
                      style="
                        background: linear-gradient(
                          to bottom,
                          #202b31 72%,
                          rgba(255, 255, 255, 0)
                        );
                      "
                    >
                      <div class="mb-2 col-md-4">
                        <label for="txtCrear" class="form-label fs-5"
                          >Agregue instrucciones</label
                        >
                      </div>
                      <div class="mb-2 col-md-8">
                        <div
                          class="row justify-content-md-end justify-content-center"
                        >
                          <!-- Grados -->
                          <div
                            @click="add_grados()"
                            class="col-4 col-md-2 d-grid mb-3"
                          >
                            <a
                              type="button"
                              value="0"
                              name=""
                              id="agregarBloqueGrad"
                              class="btn btn-secondary p-1"
                            >
                              <span>Grados</span>
                            </a>
                          </div>

                          <!-- Coordenadas -->
                          <div
                            @click="add_coordenada()"
                            class="col-4 col-md-2 d-grid mb-3"
                          >
                            <a
                              type="button"
                              value="0"
                              name=""
                              id="agregarBloqueCoor"
                              class="btn btn-secondary p-1"
                            >
                              <span>Coord</span>
                            </a>
                          </div>

                          <!-- Salidas -->
                          <div
                            @click="add_salida()" 
                            class="col-4 col-md-2 d-grid mb-3">
                            <a
                              type="button"
                              value="0"
                              name=""
                              id="agregarBloqueSal"
                              class="btn btn-secondary p-1"
                            >
                              <span>Salidas</span>
                            </a>
                          </div>

                          <!-- Entradas -->
                          <div 
                            @click="add_entrada()"
                            class="col-4 col-md-2 d-grid mb-3">
                            <a
                              type="button"
                              value="0"
                              name=""
                              id="agregarBloqueEnt"
                              class="btn btn-secondary p-1"
                            >
                              <span>Entrada</span>
                            </a>
                          </div>

                          <!-- Grip -->
                          <div 
                          @click="add_gripper()"
                          class="col-4 col-md-2 d-grid mb-3">
                            <a
                              type="button"
                              value="0"
                              name=""
                              id="agregarBloqueGrip"
                              class="btn btn-secondary p-1"
                            >
                              <span>Grip</span>
                            </a>
                          </div>
                        </div>
                      </div>
                    </div>
                    
                    
                  <!-- Linea divisora -->
                  <div class="blocksC">
                    <div
                      class="row d-flex align-items-center justify-content-center mb-3 rss"
                      id="rss0"
                      value="0"
                      v-for="(movimiento, index) in movimientos"
                      :key="movimiento"
                    >
                      <div class="col-md-1 text-center">
                        <span>{{ index }}</span>
                      </div>
                      <!-- Grados  -->
                      <div
                        v-if="movimiento.tipo == 'grado'"
                        class="col-11 col-md-9 mb-2 mb-md-0"
                      >
                        <div class="card bloque">
                          <div class="row  p-2">
                            <div class="col-6 col-md-3 mb-2">
                              <div class="input-group input-group-sm">
                                <span class="input-group-text">M0</span>
                                <input
                                  type="number"
                                  min="-360"
                                  max="360"
                                  step="0.1"
                                  class="form-control text-end"
                                  placeholder="0"
                                  value=""
                                  id="m0Bloque0"
                                  v-model="movimientos[index].m0"
                                />
                                <span class="input-group-text">°</span>
                              </div>
                            </div>
                            <div class="col-6 col-md-3 mb-2">
                              <div class="input-group input-group-sm">
                                <span class="input-group-text">M1</span>
                                <input
                                  type="number"
                                  min="-360"
                                  max="360"
                                  step="0.1"
                                  class="form-control text-end"
                                  placeholder="0"
                                  value=""
                                  id="m1Bloque0"
                                  v-model="movimientos[index].m1"
                                />
                                <span class="input-group-text">°</span>
                              </div>
                            </div>
                            <div class="col-6 col-md-3 mb-2">
                              <div class="input-group input-group-sm">
                                <span class="input-group-text">M2</span>
                                <input
                                  type="number"
                                  min="-360"
                                  max="360"
                                  step="0.1"
                                  class="form-control text-end"
                                  placeholder="0"
                                  value=""
                                  id="m2Bloque0"
                                  v-model="movimientos[index].m2"
                                />
                                <span class="input-group-text">°</span>
                              </div>
                            </div>
                            <div class="col-6 col-md-3 mb-2 mb-md-0">
                              <div class="input-group input-group-sm">
                                <span class="input-group-text">M3</span>
                                <input
                                  type="number"
                                  min="-360"
                                  max="360"
                                  step="0.1"
                                  class="form-control text-end"
                                  placeholder="0"
                                  value=""
                                  id="m3Bloque0"
                                  v-model="movimientos[index].m3"
                                />
                                <span class="input-group-text">°</span>
                              </div>
                            </div>
                            <div class="col-6 col-md-3 mb-2 mb-md-0">
                              <div class="input-group input-group-sm">
                                <span class="input-group-text">M4</span>
                                <input
                                  type="number"
                                  min="-360"
                                  max="360"
                                  step="0.1"
                                  class="form-control text-end"
                                  placeholder="0"
                                  value=""
                                  id="m4Bloque0"
                                  v-model="movimientos[index].m4"
                                />
                                <span class="input-group-text">°</span>
                              </div>
                            </div>
                            <div class="col-6 col-md-3">
                              <div class="input-group input-group-sm">
                                <span class="input-group-text">M5</span>
                                <input
                                  type="number"
                                  min="-360"
                                  max="360"
                                  step="0.1"
                                  class="form-control text-end"
                                  placeholder="0"
                                  value=""
                                  id="m5Bloque0"
                                  v-model="movimientos[index].m5"
                                />
                                <span class="input-group-text">°</span>
                              </div>
                            </div>
                          </div>
                        </div>
                      </div>
                      <!-- Coordenadas -->
                      <div v-else-if="movimiento.tipo == 'coordenada'" class="col-11 col-md-9 mb-2 mb-md-0">
                          <div class="card bloque">
                            <div class="row p-2 justify-content-center">
                              <div class="col-6 col-md-4 d-flex mb-2">
                                <div class="input-group input-group-sm">
                                  <span class="input-group-text">X</span>
                                  <input
                                    type="number"
                                    min="-360"
                                    max="360"
                                    step="0.1"
                                    class="form-control text-end"
                                    placeholder="0"
                                    value=""
                                    v-model="movimientos[index].x"
                                  />
                                  <span class="input-group-text">mm</span>
                                </div>
                              </div>
                              <div class="col-6 col-md-4 d-flex mb-2">
                                <div class="input-group input-group-sm">
                                  <span class="input-group-text">Y</span>
                                  <input
                                    type="number"
                                    min="-360"
                                    max="360"
                                    step="0.1"
                                    class="form-control text-end"
                                    placeholder="0"
                                    value=""
                                    v-model="movimientos[index].y"

                                  />
                                  <span class="input-group-text">mm</span>
                                </div>
                              </div>
                              <div class="col-6 col-md-4 d-flex mb-2">
                                <div class="input-group input-group-sm">
                                  <span class="input-group-text">Z</span>
                                  <input
                                    type="number"
                                    min="-360"
                                    max="360"
                                    step="0.1"
                                    class="form-control text-end"
                                    placeholder="0"
                                    value=""
                                    v-model="movimientos[index].z"
                                  />
                                  <span class="input-group-text">mm</span>
                                </div>
                              </div>
                            </div>
                          </div>
                      </div>
                      <!-- Salidas -->
                      <div v-else-if="movimiento.tipo == 'salida'" class="col-11 col-md-9 mb-2 mb-md-0">
                        <div  class="card bloque">
                          <div class="row p-2">
                            <div class=" col-6 col-md-4 d-flex justify-content-center mb-2">
                              <div class="form-check form-switch">
                                  <input v-model="movimientos[index].salida0" class="form-check-input" type="checkbox" >
                                  <label class="form-check-label" >Salida0</label>
                              </div>
                            </div>
                              <div class="col-6 col-md-4 d-flex justify-content-center mb-2">
                                <div class="form-check form-switch">
                                    <input v-model="movimientos[index].salida1" class="form-check-input" type="checkbox" >
                                    <label class="form-check-label" >Salida1</label>
                                </div>
                              </div>
                              <div class="col-6 col-md-4 d-flex justify-content-center mb-2">
                                <div class="form-check form-switch">
                                    <input v-model="movimientos[index].salida2" class="form-check-input" type="checkbox" >
                                    <label class="form-check-label" >Salida2</label>
                                </div>
                              </div>
                              <div class="col-6 col-md-4 d-flex justify-content-center mb-2 mb-md-0">
                                <div class="form-check form-switch">
                                      <input v-model="movimientos[index].salida3" class="form-check-input" type="checkbox" >
                                      <label class="form-check-label" >Salida3</label>
                                </div>
                              </div>
                              <div class="col-6 col-md-4 d-flex justify-content-center">
                                <div class="form-check form-switch">
                                    <input v-model="movimientos[index].salida4" class="form-check-input" type="checkbox" >
                                    <label class="form-check-label" >Salida4</label>
                                </div>
                              </div>
                            </div>
                          </div>
                        </div>

                      <!-- Entradas -->
                    <div v-else-if="movimiento.tipo == 'entrada'" class="col-11 col-md-9 mb-2 mb-md-0">
                    <div class="card bloque">
                        <div class="row p-2 justify-content-center">
                            <div class="col-7 col-md-7 mb-2">
                                <div class="input-group input-group-sm">
                                    <label class="input-group-text">Selcciona entrada</label>
                                    <select v-model="movimientos[index].entrada_seleccionada" class="form-select">
                                        <option value="0">Entrada0</option>
                                        <option value="1">Entrada1</option>
                                        <option value="2">Entrada2</option>
                                        <option value="3">Entrada3</option>
                                        <option value="4">Entrada4</option>
                                    </select>
                                </div>
                            </div>
                            
                            <div class="col-6 col-md-6">
                                <div class="input-group input-group-sm justify-content-center">
                                    <label class="px-1 px-md-3">If entrada:</label>
                                    <div class="form-check form-check-inline">
                                        <input v-model="movimientos[index].valor_entrada" class="form-check-input" type="radio" name="rOptions`+ num +`" id="0Bloque`+ num +`" value="0" checked>
                                        <label class="form-check-label">0</label>
                                    </div>
                                    <div class="form-check form-check-inline">
                                        <input v-model="movimientos[index].valor_entrada" class="form-check-input" type="radio" name="rOptions`+ num +`" id="1Bloque`+ num +`" value="1">
                                        <label  class="form-check-label">1</label>
                                    </div>
                                    
                                </div>
                            </div>
                            <div class="col-6 col-md-5">
                                <div class="input-group input-group-sm">
                                    <label class="input-group-text">Continuar en</label>
                                    <input v-model="movimientos[index].continuar_en" type="number" min="1" max="1000" class="form-control text-center" placeholder="Bloque" value="" id="continueBloque`+ num +`">
                                </div>
                            </div>
                        </div>
                    </div>
                    </div>

                    <!-- Griper -->
                    <div v-else-if="movimiento.tipo == 'ipper'" class="col-11 col-md-9 mb-2 mb-md-0">
                      <div class="card bloque">
                        <div class="row p-2 justify-content-center">
                          <div class="col-md-9 align-self-center mb-2 mb-md-0">
                              <div class="input-group">
                                  <label class="form-label mb-0 px-3" >Gripper</label>
                                  <input v-model="movimientos[index].valor_entrada" type="range" value="0" class="form-range form-range2 mt-1" min="0" max="30" oninput="this.nextElementSibling.value = this.value" style="width: 60%;">
                                  <output  class="text-end" style="margin-left: 1rem; min-width: 1rem;">0</output><span class="mx-1">cm</span>
                              </div>
                            </div>
                        </div>
                      </div>
                    </div>
                    
                    <!-- Flechas de mov -->
                    <div class="col-4 col-md-1">
                      <div class="d-flex flex-column">
                        <div
                          @click="arriba_bloque(index)"
                          class="upBloque"
                        ></div>
                        <div
                          @click="abajo_bloque(index)"
                          class="downBloque"
                        ></div>
                      </div>
                    </div>
                    <!-- Flecha para eliminar bloque -->
                    <div class="col-2 col-md-1">
                      <div class="d-flex flex-column">
                        <div class="d-flex justify-content-center">
                          <div
                            @click="eliminar_bloque(index)"
                            class="imgElim d-flex justify-content-center eliminarBloque"
                          ></div>
                        </div>
                      </div>
                    </div>
                  </div>

                </div>
                <!-- Linea divisora -->
                <div style="height: 0.3vh; background-color: #4c5155"></div>
              </div>
              </div>
              </div>

              <div class="row justify-content-between">
                <div class="col-auto mb-2">
                  <a
                    class="btn btn-secondary px-3 fs-5"
                    id="btnComoCrear"
                    style="min-width: 3rem"
                    >?</a
                  >
                </div>
                <div 
                  @click="ejecutar_path()"
                  class="col-auto offset-sm-3 mb-2">
                  <a
                    class="btn btn-secondary py-1 px-3 fs-6"
                    name="pruebaCrear"
                    id="pruebaCrear"
                    style="max-height: 2rem"
                    >Ejecutar</a
                  >
                </div>
                <div class="col-12 col-md-5">
                  <div class="input-group mb-4 mb-sm-2">
                    <input
                      type="text"
                      class="form-control"
                      placeholder="Nombre archivo"
                      aria-describedby="guardarArchivo"
                      id="nombreArch"
                      v-model="nombreArchivo"
                      style="max-height: 2rem; border: 1px solid #ced4da"
                    />
                    <a
                      class="btn btn-secondary px-3 px-sm-4 px-md-2 px-xl-3 py-1"
                      id="guardarArchivo"
                      style="max-height: 2rem"
                      @click="guardarArchivo()"
                      >Guardar</a
                    >
                  </div>
                </div>
              </div>
            </div>

            <div
              class="container rounded"
              id="comoCrear"
              style="margin-top: 1.8rem; display: none"
            >
              <div class="row">
                <div class="col-md-1 mb-4">
                  <a
                    class="btn btn-secondary px-1 fs-5"
                    id="regresar"
                    style="min-width: 3rem"
                    >🡳</a
                  >
                </div>
                <div class="col-md-12 mb-4">
                  <div class="mb-4">
                    <span class="mb-3 fs-5">Por motor</span>
                    <p>Instrucciones...</p>
                  </div>
                  <div class="mb-4">
                    <span class="mb-3 fs-5">Con cooredenadas</span>
                    <p>Instrucciones...</p>
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
    if (localStorage.getItem("Lista_movimientos")){
      let listaDeBloques = JSON.parse(localStorage.getItem("Lista_movimientos")) 
      let length = listaDeBloques.length
      
      for(let i = 0; i < length; i++){
        if(listaDeBloques[i].tipo == "salida"){
          console.log(listaDeBloques[i])
          this.newSalida["delay"] = listaDeBloques[i].delay
          this.newSalida["salida0"] = listaDeBloques[i].salidas[0]
          this.newSalida["salida1"] = listaDeBloques[i].salidas[1]
          this.newSalida["salida2"] = listaDeBloques[i].salidas[2]
          this.newSalida["salida3"] = listaDeBloques[i].salidas[3]
          this.newSalida["salida4"] = listaDeBloques[i].salidas[4]
          this.movimientos.push(this.newSalida)
          
        }else if(listaDeBloques[i].tipo == "grado"){
          console.log(listaDeBloques[i])
          console.log("Delay" + listaDeBloques[i].delay)
          console.log("velocidad" + listaDeBloques[i].velocidad)
          console.log("M3" + listaDeBloques[i].angulos[2])

          this.newGrados["delay"] = listaDeBloques[i].delay
          this.newGrados["m0"] = listaDeBloques[i].angulos[0]
          this.newGrados["m1"] = listaDeBloques[i].angulos[1]
          this.newGrados["m2"] = listaDeBloques[i].angulos[2]
          this.newGrados["m3"] = listaDeBloques[i].angulos[3]
          this.newGrados["m4"] = listaDeBloques[i].angulos[4]
          this.newGrados["m5"] = listaDeBloques[i].angulos[5]
          this.newGrados["vel"] = listaDeBloques[i].velocidad
          this.movimientos.push(this.newGrados)

        }else if(listaDeBloques[i].tipo == "coordenada"){
          console.log(listaDeBloques[i])
          this.newCoordenada["delay"] = listaDeBloques[i].delay
          this.newCoordenada["x"] = listaDeBloques[i].paths[0]
          this.newCoordenada["y"] = listaDeBloques[i].paths[1]
          this.newCoordenada["z"] = listaDeBloques[i].paths[2]
          this.newCoordenada["vel"] = listaDeBloques[i].velocidad 
          this.movimientos.push(this.newCoordenada)

        }else if(listaDeBloques[i].tipo == "entrada"){
          this.newEntrada["delay"] = listaDeBloques[i].delay
          this.newEntrada["entrada_seleccionada"] = listaDeBloques.entrada_select
          this.newEntrada["continuar_en"] = listaDeBloques.continuar_en
          this.newEntrada["valor_entrada"] = listaDeBloques.valor_entrada
          this.movimientos.push(this.newEntrada)

        }else if(listaDeBloques[i].tipo == "gripper"){
          console.log(listaDeBloques[i])
          this.newGripper["delay"] = listaDeBloques.delay
          this.newGripper["valor_entrada"] = listaDeBloques.apertura
          this.movimientos.push(this.newGripper)

        }
        else{
          alert("No existe la entrada")
        }
      }
      
      //localStorage.clear() // ---> No se si mantenerlo 
  
    }else{
      alert("Local Storage vacio")
    }

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

  data() {
    return {
      movimientos: [],
      newGrados: {
        tipo: 'grado',
        m0: 0,
        m1: 0,
        m2: 0,
        m3: 0,
        m4: 0,
        m5: 0,
        vel: 0,
        delay: 0,
      },
      newCoordenada: {
        tipo: 'coordenada',
        x: 0,
        y: 0,
        z: 0,
        vel: 0,
        delay: 0,
      },
      newSalida: { 
        tipo: "salida", 
        salida0: 0,
        salida1: 0,
        salida2: 0,
        salida3: 0,
        salida4: 0,
        delay: 0 
      },
      newEntrada: {
        tipo: "entrada",
        entrada_seleccionada: 0, 
        continuar_en: 0,
        valor_entrada: 0,  
        delay: 0,
      }, 
      newGripper: {
        tipo: "ipper",
        valor_entrada: 0,  
        delay: 0,
      },

      nombreArchivo: "",
      archivoGuardado: ["",""],

      //Ros
      ros: new ROSLIB.Ros({
        url: "ws:/localhost:9090"
      })
    }
  },

  methods: {
    add_grados() {
      this.movimientos.push(JSON.parse(JSON.stringify(this.newGrados)))
    },

    add_coordenada() {
      this.movimientos.push(JSON.parse(JSON.stringify(this.newCoordenada)))
    },
    add_salida(){
      this.movimientos.push(JSON.parse(JSON.stringify(this.newSalida)))
    }, 
    add_entrada(){ 
      this.movimientos.push(JSON.parse(JSON.stringify(this.newEntrada)))
    },
    add_gripper(){ 
      this.movimientos.push(JSON.parse(JSON.stringify(this.newGripper)))
    },
    //Disminuye en 1 la posicion del bloque y en esa posicion crea una copia de 
    // la cadena original, luego elimina el original : 
    arriba_bloque(index){
      if (index != 0){
        this.movimientos.splice(index - 1, 0, this.movimientos[index])
        this.movimientos.splice(index + 1, 1)
      }
    },
    //Hace una copia del bloque, en dos posiciones superiores a este, luego se elimina 
    // a el original. 
    abajo_bloque(index){
      this.movimientos.splice(index + 2, 0, this.movimientos[index])
      this.movimientos.splice(index , 1)
    },
    eliminar_bloque(index){
      // Elimina el bloque en la posicion index
      this.movimientos.splice(index, 1)
    },

    ejecutar_path(){      
      var sliders_value = new ROSLIB.Topic({
          ros: this.ros, 
          name: '/secuencia_mov',
          messageType: 'std_msgs/String'
      });
      var setpoints = new ROSLIB.Message({
          data: JSON.stringify(this.movimientos)   
      })
      sliders_value.publish(setpoints)
      
      console.log(this.setpoints)
    }, 

    guardarArchivo(){
      var archivoGuardado = new ROSLIB.Topic({
        ros: this.ros, 
        name: '/guardar_archivo', 
        messageType: "std_msgs/Strings"
      });      
      
      if(this.movimientos.length < 1 ){
        alert("La entrada de bloques se encuentra vacía")
      }else if(this.nombreArchivo.length == 0){
        alert("El archivo no tiene nombre")
      }
      else{
          this.archivoGuardado[0] = this.nombreArchivo
          this.archivoGuardado[1] = this.movimientos
          console.log(this.archivoGuardado)

          var payload = new ROSLIB.Message({
          data: JSON.stringify(this.archivoGuardado) 
          })
        
          archivoGuardado.publish(payload)
      }

      
    }

  },
}
</script>
