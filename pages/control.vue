<template>
  <div>
    <div
      class="alert alert-warning fixed-top text-center"
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
      No se puede pasar de este valor
    </div>
    <div
      class="alert alert-warning fixed-top text-center"
      role="alert"
      id="alerta2"
      style="
        display: none;
        left: 50%;
        transform: translateX(-50%);
        width: 30%;
        margin-top: 2rem;
      "
    >
      Robot en posición no apta para esta carga
    </div>

    <div class="container-fluid px-sm-5 py-3 py-sm-0">
      <div class="row g-5 my-sm-2">
        <div class="col-md-12">
          <div
            class="card p-sm-3 bg-secondary shadow-sm d-flex rounded card-artic"
          >
            <div>
              <p class="fs-6 px-3 pt-3 p-sm-0">Articulaciones</p>
            </div>
            <!--Inputs range-->
            <!-- v-for recorre los valores de setpoints, index devuelve la posicion de la key del objeto:  -->
            <div class="container mb-3 mb-sm-0">
              <div class="row" v-for="(motor, index) in motores" :key="motor">
                <div class="col-md-2">
                  <p class="text-center fw-bold">{{ motor }}</p>
                </div>
                <!-- Articualcion 0, 2, 4, 5 -->
                <div
                  v-if="index == 0 || index == 2 || index == 4 || index == 5"
                  class="col-md-10 d-flex justify-content-center"
                >
                  <input
                    v-model="setpoints[index].setpoint"
                    type="range"
                    value="0"
                    class="form-range slider"
                    min="-90"
                    max="90"
                    oninput="this.nextElementSibling.value = this.value"
                    onmouseup="this.nextElementSibling.value = this.value"
                    onkeydown="return false;"
                  />
                  <output
                    class="text-end"
                    style="margin-left: 1rem; min-width: 2rem"
                    >{{ setpoints[index].setpoint }}</output
                  ><span
                    style="
                      font-size: 1rem;
                      margin-right: 1rem;
                      margin-left: 0.5rem;
                    "
                    >°</span
                  >
                </div>
                <!-- Articualcion1  -->
                <div
                  v-else-if="index == 1"
                  class="col-md-10 d-flex justify-content-center"
                >
                  <input
                    v-model="setpoints[index].setpoint"
                    type="range"
                    value="0"
                    class="form-range slider"
                    min="-80"
                    max="80"
                    oninput="this.nextElementSibling.value = this.value"
                    onmouseup="this.nextElementSibling.value = this.value"
                    onkeydown="return false;"
                  />
                  <output
                    class="text-end"
                    style="margin-left: 1rem; min-width: 2rem"
                    >{{ setpoints[index].setpoint }}</output
                  ><span
                    style="
                      font-size: 1rem;
                      margin-right: 1rem;
                      margin-left: 0.5rem;
                    "
                    >°</span
                  >
                </div>

                <div v-else class="col-md-10 d-flex justify-content-center">
                  <input
                    v-model="setpoints[index].setpoint"
                    type="range"
                    value="0"
                    class="form-range slider"
                    min="-75"
                    max="75"
                    oninput="this.nextElementSibling.value = this.value"
                    onmouseup="this.nextElementSibling.value = this.value"
                    onkeydown="return false;"
                  />
                  <output
                    class="text-end"
                    style="margin-left: 1rem; min-width: 2rem"
                    >{{ setpoints[index].setpoint }}</output
                  ><span
                    style="
                      font-size: 1rem;
                      margin-right: 1rem;
                      margin-left: 0.5rem;
                    "
                    >°</span
                  >
                </div>
              </div>

              <!-- Botones de ejecutar -->
              <div class="row">
                <div class="col-md-2">
                  <p class="text-center fw-bold">{{ motor }}</p>
                </div>
                <div class="col-md-10 d-flex justify-content-end">
                  <!-- Ejecutar -->
                  <button
                    @click="publish_sliders_value()"
                    type="button"
                    class="btn btn-secondary"
                    value=""
                    style="
                      padding: 2vh;
                      margin-right: 1em;
                      background: #488fb1;
                      border-width: 0px;
                    "
                  >
                    Ejecutar
                  </button>

                  <button
                    @click="send_home()"
                    type="button"
                    class="btn btn-secondary"
                    value=""
                    style="
                      padding: 2vh;
                      margin-right: 1em;
                      background: #488fb1;
                      border-width: 0px;
                    "
                  >
                    Home
                  </button>

                  <button
                    @click="_fcn_gripper()"
                    type="button"
                    class="btn btn-secondary"
                    value=""
                    style="padding: 1vh"
                  >
                    Gripper
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="col-md-4">
          <!--Input Coordenadas-->
          <div
            class="card p-3 bg-secondary shadow-sm d-flex rounded"
            style="min-height: 13.79rem"
          >
            <div>
              <p class="fs-6 mb-3">Coordenadas</p>
            </div>
            <div
              class="row gy-4 px-3 justify-content-center"
              v-for="(coord, index) in coordinates_motor"
              :key="coord"
            >
              <div class="col-12 col-xl-10" style="text-align: center">
                <div class="input-group input-group-sm">
                  <span class="input-group-text">{{ coord }}</span>
                  <input
                    v-model="coordinates[index].coordinate"
                    type="number"
                    min="-360"
                    max="360"
                    step="0.1"
                    class="form-control text-center"
                    placeholder=""
                    value=""
                  />
                  <span class="input-group-text">mm</span>
                </div>
              </div>
            </div>
            <button
              @click="go_to_pose_goal()"
              type="button"
              class="btn btn-secondary"
              value=""
              style="padding: 1vh"
            >
              coordenada
            </button>
          </div>
        </div>
        <div class="col-md-8">
          <!--Input botones-->
          <div class="card p-3 pb-sm-2 bg-secondary shadow-sm d-flex rounded">
            <div>
              <p class="fs-6 mb-2">Controles</p>
              <div class="container">
                <div
                  class="row d-flex align-items-center"
                  style="min-height: 10.17rem"
                >
                  <div class="col-md-4">
                    <div class="container">
                      <div class="d-flex flex-column">
                        <div class="d-flex justify-content-center mb-3">
                          <input
                            @mousedown="go_to_vertical_up_start()"
                            @mouseup="go_to_vertical_up_finish()"
                            type="image"
                            src="arrow.svg"
                            value="0"
                            name="vUp"
                            id="vUp"
                            class="arrows-v1"
                            draggable="false"
                          />
                        </div>
                        <div class="d-flex justify-content-center">
                          <input
                            @mousedown="go_to_vertical_down_start()"
                            @mouseup="go_to_vertical_down_finish()"
                            type="image"
                            src="arrow.svg"
                            value="0"
                            name="vDown"
                            id="vDown"
                            class="arrows-v2"
                            draggable="false"
                          />
                        </div>
                      </div>
                    </div>
                    <div
                      class="position-relative mb-4 mb-md-0"
                      style="height: 2rem"
                    >
                      <span
                        class="position-absolute bottom-0 start-50 translate-middle-x"
                        >Vertical</span
                      >
                    </div>
                  </div>
                  <div class="col-md-4">
                    <div class="container">
                      <div class="row">
                        <div
                          class="col-4 d-flex justify-content-center align-items-center"
                        >
                          <input
                            type="image"
                            src="arrow.svg"
                            value="2"
                            name="hLeft"
                            id="hLeft"
                            class="arrows-h1"
                            draggable="false"
                          />
                        </div>
                        <div class="col-4 d-flex justify-content-center">
                          <div class="d-flex flex-column">
                            <div class="d-flex justify-content-center mb-3">
                              <input
                                type="image"
                                src="arrow.svg"
                                value="3"
                                name="hForward"
                                id="hForward"
                                class="arrows-h2"
                                draggable="false"
                              />
                            </div>
                            <div class="d-flex justify-content-center">
                              <input
                                type="image"
                                src="arrow.svg"
                                value="4"
                                name="hBackward"
                                id="hBackward"
                                class="arrows-h3"
                                draggable="false"
                              />
                            </div>
                          </div>
                        </div>
                        <div
                          class="col-4 d-flex justify-content-center align-items-center"
                        >
                          <input
                            type="image"
                            src="arrow.svg"
                            value="5"
                            name="hRight"
                            id="hRight"
                            class="arrows-h4"
                            draggable="false"
                          />
                        </div>
                      </div>
                    </div>
                    <div class="position-relative" style="height: 2rem">
                      <span
                        class="position-absolute bottom-0 start-50 translate-middle-x"
                        >Horizontal</span
                      >
                    </div>
                  </div>
                  <div class="col-md-4">
                    <div class="container">
                      <div class="row alineacion-v-rotacion">
                        <div class="col-6 d-flex justify-content-end">
                          <input
                            type="image"
                            src="arrow.svg"
                            value="6"
                            name="rLeft"
                            id="rLeft"
                            class="arrows-r1"
                            draggable="false"
                          />
                        </div>
                        <div class="col-6 d-flex justify-content-start">
                          <input
                            type="image"
                            src="arrow.svg"
                            value="7"
                            name="rRight"
                            id="rRight"
                            class="arrows-r2"
                            draggable="false"
                          />
                        </div>
                      </div>
                    </div>
                    <div class="position-relative" style="height: 4rem">
                      <span
                        class="position-absolute bottom-0 start-50 translate-middle-x"
                        >Rotación</span
                      >
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
  mounted() {
    var ros = new ROSLIB.Ros({
      url: 'ws:/localhost:9090',
    })
    ros.on('connection', () => {
      console.log('Connected to websocket')
    })
    ros.on('error', (error) => {
      console.log('Error connecting: ', error)
    })
    ros.on('close', () => {
      console.log('Se cerro la conexion')
    })
  },
  data() {
    return {
      motores: [
        'motor 0',
        'motor 1',
        'motor 2',
        'motor 3',
        'motor 4',
        'motor 5',
      ],
      setpoints: [
        { setpoint: 0 },
        { setpoint: 0 },
        { setpoint: 0 },
        { setpoint: 0 },
        { setpoint: 0 },
        { setpoint: 0 },
      ],
      gripper: 0,

      coordinates_motor: ['Z', 'Y', 'X'],
      coordinates: [{ coordinate: 0 }, { coordinate: 0 }, { coordinate: 0 }],
      vertical: [{ verticals: 0 }, { verticals: 0 }],

      ros: new ROSLIB.Ros({
        url: 'ws:/localhost:9090',
      }),
    }
  },
  methods: {
    // Envio de los setpoints de los sliders
    publish_sliders_value() {
      var sliders_value = new ROSLIB.Topic({
        ros: this.ros,
        name: '/sliders_value',
        messageType: 'geometry_msgs/Twist',
      })
      var setpoints = new ROSLIB.Message({
        data: JSON.stringify(this.setpoints),
      })

      sliders_value.publish(setpoints)
      console.log(this.setpoints)
    },
    send_home() {
      var send_home = new ROSLIB.Topic({
        ros: this.ros,
        name: '/send_home',
        messageType: 'geometry_msgs/Twist',
      })
      var setpoint = new ROSLIB.Message({
        data: JSON.stringify(this.setpoint),
      })
      for (let i = 0; i < 6; i++) {
        this.setpoints[i].setpoint = 0
      }

      send_home.publish(setpoint)
    },
    _fcn_gripper() {
      var send_gripper = new ROSLIB.Topic({
        ros: this.ros,
        name: '/gripper',
        messageType: 'geometry_msgs/Twist',
      })
      var gripper = new ROSLIB.Message({
        data: JSON.stringify(this.gripper),
      })
      if (this.gripper == 0) {
        this.gripper = 1
      } else {
        this.gripper = 0
      }
      send_gripper.publish(gripper)
      console.log(this.gripper)
    },
    go_to_pose_goal() {
      var end_efector = new ROSLIB.Topic({
        ros: this.ros,
        name: '/end_efector',
        messageType: 'geometry_msgs/Twist',
      })
      var coordinates = new ROSLIB.Message({
        data: JSON.stringify(this.coordinates),
      })
      end_efector.publish(coordinates)
      console.log(this.coordinates)
    },
    go_to_vertical_up_start() {
      var vertical_up = new ROSLIB.Topic({
        ros: this.ros,
        name: '/vertical_start',
        messageType: 'std_msgs/String',
      })
      var go_vertical_up = new ROSLIB.Message({
        data: JSON.stringify(1),
      })

      // while (go_vertical_up == 1){
      //     while (i <= 90) {
      //         motor = motor + 1
      //         i = i + 1
      //     }

      // console.log(motor)
      // }

      vertical_up.publish(go_vertical_up)
      console.log(go_vertical_up)
    },
    go_to_vertical_up_finish() {
      var vertical_down = new ROSLIB.Topic({
        ros: this.ros,
        name: '/vertical_finish',
        messageType: 'std_msgs/Twist',
      })
      var go_vertical = new ROSLIB.Message({
        data: JSON.stringify(0),
      })
      vertical_down.publish(go_vertical)
      console.log(go_vertical)
    },
    go_to_vertical_down_start() {
      var vertical = new ROSLIB.Topic({
        ros: this.ros,
        name: '/vertical_down_start',
        messageType: 'std_msgs/Twist',
      })
      var go_vertical_down = new ROSLIB.Message({
        data: JSON.stringify(1),
      })
      vertical.publish(go_vertical_down)
      console.log(go_vertical_down)
    },

    go_to_vertical_down_finish() {
      var vertical = new ROSLIB.Topic({
        ros: this.ros,
        name: '/vertical_down_finish',
        messageType: 'std_msgs/Twist',
      })
      var go_vertical_down = new ROSLIB.Message({
        data: JSON.stringify(0),
      })
      vertical.publish(go_vertical_down)
      console.log(go_vertical_down)
    },
  },
}
</script>
