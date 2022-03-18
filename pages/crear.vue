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
                  <div class="blocksC">
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
                          <div class="col-4 col-md-2 d-grid mb-3">
                            <a
                              type="button"
                              value="0"
                              name=""
                              id="agregarBloqueGrad"
                              class="btn btn-secondary p-1"
                            >
                              <span @click="add_grados()">Grados</span>
                            </a>
                          </div>
                          <div class="col-4 col-md-2 d-grid mb-3">
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
                          <div class="col-4 col-md-2 d-grid mb-3">
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
                          <div class="col-4 col-md-2 d-grid mb-3">
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
                          <div class="col-4 col-md-2 d-grid mb-3">
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

                    <!-- Grados  -->
                    <div
                      class="row d-flex align-items-center justify-content-center mb-3 rss"
                      id="rss0"
                      value="0"
                      v-for="instr in instr_grados" :key="instr"
                    >
                      <div class="col-md-1 text-center">
                        <span>{{newGrados.id}}</span>
                      </div>
                      <div class="col-11 col-md-9 mb-2 mb-md-0" >
                        <div class="card bloque">
                          <div class="row p-2">
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
                                />
                                <span class="input-group-text">°</span>
                              </div>
                            </div>
                            <div class="col-6 col-md-3 mb-2">
                              <div class="input-group input-group-sm">
                                <span class="input-group-text">Vel</span>
                                <input
                                  type="number"
                                  min="1"
                                  max="100"
                                  step="0.1"
                                  class="form-control form-control-vel text-end"
                                  placeholder="1"
                                  value="1"
                                  id="velBloque0"
                                />
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
                                />
                                <span class="input-group-text">°</span>
                              </div>
                            </div>
                            <div class="col-6 col-md-3">
                              <div class="input-group input-group-sm">
                                <span class="input-group-text">Delay</span>
                                <input
                                  type="number"
                                  min="0"
                                  max="1000"
                                  step="0.1"
                                  class="form-control text-end"
                                  placeholder="0"
                                  value=""
                                  id="delayBloque0"
                                />
                              </div>
                            </div>
                          </div>
                        </div>
                      </div>
                      <div class="col-4 col-md-1">
                        <div class="d-flex flex-column">
                          <div class="upBloque" id="upBloque0"></div>
                          <div class="downBloque" id="downBloque0"></div>
                        </div>
                      </div>
                      <div class="col-2 col-md-1">
                        <div class="d-flex flex-column">
                          <div class="d-flex justify-content-center">
                            <div
                              class="imgElim d-flex justify-content-center eliminarBloque"
                              id="eliminarBloque0"
                            ></div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div style="height: 0.3vh; background-color: #4c5155"></div>
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
                <div class="col-auto offset-sm-3 mb-2">
                  <a
                    class="btn btn-secondary py-1 px-3 fs-6"
                    name="pruebaCrear"
                    id="pruebaCrear"
                    style="max-height: 2rem"
                    >Probar</a
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
                      style="max-height: 2rem; border: 1px solid #ced4da"
                    />
                    <a
                      class="btn btn-secondary px-3 px-sm-4 px-md-2 px-xl-3 py-1"
                      id="guardarArchivo"
                      style="max-height: 2rem"
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
  data(){
    return{
      instr_grados: [],
      newGrados: {
        id: 0,
        m0: '',
        m1: '',
        m2: '',
        m3: '',
        m4: '',
        m5: '',
        vel: '',
        delay: ''
      }
    }
  },

  methods: {
    add_grados(){           
      this.instr_grados.push(this.newGrados)
    }
  }
}
</script>