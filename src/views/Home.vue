<template>
  <el-container class="home-container">
    <el-header>
      <h1>
        Driverbot
      </h1>
    </el-header>
    <el-main>
      <el-tabs>
        <el-tab-pane label="Home">
          <el-card class="box-card" v-loading="!connected">
            <h1>
              Drive
            </h1>
            <el-row>
              <el-col :offset="9" :span="2">
                <el-button v-if="isActive(1, 1)" @click="setActive(1, 1)" type="primary" icon="el-icon-top-left" circle></el-button>
                <el-button v-else @click="setActive(1, 1)" icon="el-icon-top-left" circle></el-button>
              </el-col>
              <el-col :span="2">
                <el-button v-if="isActive(1, 0)" @click="setActive(1, 0)" type="primary" icon="el-icon-top" circle></el-button>
                <el-button v-else @click="setActive(1, 0)" icon="el-icon-top" circle></el-button>
              </el-col>
              <el-col :span="2">
                <el-button v-if="isActive(1, -1)" @click="setActive(1, -1)" type="primary" icon="el-icon-top-right" circle></el-button>
                <el-button v-else @click="setActive(1, -1)" icon="el-icon-top-right" circle></el-button>
              </el-col>
            </el-row>
            <el-row>
              <el-col :offset="9" :span="2">
                <el-button v-if="isActive(0, 1)" @click="setActive(0, 1)" type="primary" icon="el-icon-back" circle></el-button>
                <el-button v-else @click="setActive(0, 1)" icon="el-icon-back" circle></el-button>
              </el-col>
              <el-col :span="2">
                <el-button v-if="isActive(0, 0)" @click="setActive(0, 0)" type="primary" icon="el-icon-close" circle></el-button>
                <el-button v-else @click="setActive(0, 0)" icon="el-icon-close" circle></el-button>
              </el-col>
              <el-col :span="2">
                <el-button v-if="isActive(0, -1)" @click="setActive(0, -1)" type="primary" icon="el-icon-right" circle></el-button>
                <el-button v-else @click="setActive(0, -1)" icon="el-icon-right" circle></el-button>
              </el-col>
            </el-row>
            <el-row>
              <el-col :offset="9" :span="2">
                <el-button v-if="isActive(-1, 1)" @click="setActive(-1, 1)" type="primary" icon="el-icon-bottom-left" circle></el-button>
                <el-button v-else @click="setActive(-1, 1)" icon="el-icon-bottom-left" circle></el-button>
              </el-col>
              <el-col :span="2">
                <el-button v-if="isActive(-1, 0)" @click="setActive(-1, 0)" type="primary" icon="el-icon-bottom" circle></el-button>
                <el-button v-else @click="setActive(-1, 0)" icon="el-icon-bottom" circle></el-button>
              </el-col>
              <el-col :span="2">
                <el-button v-if="isActive(-1, -1)" @click="setActive(-1, -1)" type="primary" icon="el-icon-bottom-right" circle></el-button>
                <el-button v-else @click="setActive(-1, -1)" icon="el-icon-right" circle></el-button>
              </el-col>
            </el-row>
          </el-card>
          <el-card class="box-card" v-loading="!connected">
            <h1>
              Info
            </h1>
            <el-table :data="tableData" style="width: 100%">
              <el-table-column prop="name"> </el-table-column>
              <el-table-column prop="value"> </el-table-column>
            </el-table>
          </el-card>
          <el-card class="box-card" v-loading="!connected">
            <h1>
              Logger
            </h1>
            <el-input id="logger" type="textarea" :rows="2" v-model="logger" readonly></el-input>
          </el-card>
        </el-tab-pane>
        <el-tab-pane label="Config">
          <el-card class="box-card">
            <h1>
              MQTT Settings
            </h1>
            <el-form ref="form" :model="form" label-width="120px" label-position="left">
              <el-form-item label="Host">
                <el-input v-model="form.host"></el-input>
              </el-form-item>
              <el-form-item label="Port">
                <el-input-number v-model="form.port" :min="0" :max="9999" controls-position="right"></el-input-number>
              </el-form-item>
              <el-form-item label="Endpoint">
                <el-input v-model="form.endpoint"></el-input>
              </el-form-item>
              <el-form-item label="Clean">
                <el-switch v-model="form.clean"></el-switch>
              </el-form-item>
              <el-form-item label="Connect Timeout">
                <el-input-number v-model="form.connectTimeout" :min="0" controls-position="right"></el-input-number>
              </el-form-item>
              <el-form-item label="Reconnect Period">
                <el-input-number v-model="form.reconnectPeriod" :min="0" controls-position="right"></el-input-number>
              </el-form-item>
              <el-form-item label="Client ID">
                <el-input v-model="form.clientId"></el-input>
              </el-form-item>
              <el-form-item label="Username">
                <el-input v-model="form.username"></el-input>
              </el-form-item>
              <el-form-item label="Password">
                <el-input v-model="form.password"></el-input>
              </el-form-item>
              <el-form-item>
                <el-button type="primary" @click="reconnect">{{ connected ? 'Reconnect' : 'Connect' }}</el-button>
              </el-form-item>
            </el-form>
          </el-card>
        </el-tab-pane>
        <el-tab-pane label="About">
          <el-card class="box-card">
            <h1>About</h1>
            <el-row>
              <el-col :span="8">
                <el-card :body-style="{ padding: '0px' }">
                  <img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png" height="180" class="image" />
                  <div style="padding: 14px;">
                    <span>Link to Github repo</span>
                    <div class="bottom">
                      <el-link href="https://github.com/abbindustrigymnasium/driverbot-abbadanor" type="primary">Github</el-link>
                    </div>
                  </div>
                </el-card>
              </el-col>
              <el-col :span="8">
                <el-card :body-style="{ padding: '0px' }">
                  <img src="https://brandeps.com/logo-download/V/Vue-JS-logo-vector-01.svg" height="180" class="image" />
                  <div style="padding: 14px;">
                    <span>Created with Vue 3</span>
                    <div class="bottom">
                      <el-link href="https://v3.vuejs.org/" type="primary">Vue 3</el-link>
                    </div>
                  </div>
                </el-card>
              </el-col>
              <el-col :span="8">
                <el-card :body-style="{ padding: '0px' }">
                  <img src="https://cdn.worldvectorlogo.com/logos/element-ui-1.svg" height="180" class="image" />
                  <div style="padding: 14px;">
                    <span>Using ElementUI</span>
                    <div class="bottom">
                      <el-link href="https://element.eleme.io/#/en-US" type="primary">Element UI</el-link>
                    </div>
                  </div>
                </el-card>
              </el-col>
            </el-row>
          </el-card>
        </el-tab-pane>
      </el-tabs>
    </el-main>
    <el-footer>
      <p>
        Adam Nord 2021
      </p>
    </el-footer>
  </el-container>
</template>

<script>
import mqtt from 'mqtt'
export default {
  name: 'Home',
  data() {
    return {
      connection: {
        host: 'broker.hivemq.com',
        port: 8000,
        endpoint: '/mqtt',
        clean: true,
        connectTimeout: 4000,
        reconnectPeriod: 0,
        clientId: 'mqttjs_3be2c321',
        username: 'abbadanor',
        password: 'euYB9zYt9jDKKb6',
      },
      publish: {
        topic: 'drive',
        qos: 0,
        payload: 'hello',
      },
      client: {
        connected: false,
      },
      connected: false, // vue reactivity workaround
      direction: {
        x: 0,
        y: 0,
      },
      value: {
        x: 0,
        y: 105,
      },
      driveDirection: 0, // -1, 0, 1
      turnDirection: 0, // -1, 0, 1
      tableData: [],
      logger: '',
      form: {
        host: '',
        port: 0,
        endpoint: '/',
        clean: false,
        connectTimeout: 0,
        reconnectPeriod: 0,
        clientId: '',
        username: '',
        password: '',
      },
    }
  },
  methods: {
    createConnection() {
      const { host, port, endpoint, ...options } = this.connection
      const connectUrl = `ws://${host}:${port}${endpoint}`
      try {
        this.client = mqtt.connect(connectUrl, options)
        this.logger = ''
      } catch (error) {
        console.error('mqtt connection error', error)
      }
      this.client.on('connect', () => {
        console.log('Connection succeded!')
        this.connected = this.client.connected

        //wtf
        let capitalize = string =>
          string
            .split(/(?=[A-Z])/)
            .join(' ')
            .charAt(0)
            .toUpperCase() +
          string
            .split(/(?=[A-Z])/)
            .join(' ')
            .slice(1)

        if (this.tableData === []) {
          for (const key in this.connection) {
            this.tableData.push({
              name: capitalize(key),
              value: this.connection[key],
            })
          }
        } else {
          this.tableData = []
          for (const key in this.connection) {
            this.tableData.push({
              name: capitalize(key),
              value: this.connection[key],
            })
          }
        }

        this.form = this.connection
      })
      this.client.on('error', error => {
        console.log('Connection failed', error)
      })
    },
    doPublish() {
      const { topic, qos, payload } = this.publish
      this.client.publish(topic, payload, qos, error => {
        if (error) {
          console.log('Publish error', error)
        }
      })
    },
    reconnect() {
      if (this.client.connected) {
        try {
          this.client.end()
          this.client = {
            connected: false,
          }
          this.connected = false
          console.log('Successfully disconnected!')
        } catch (error) {
          console.log('Disconnect failed', error.toString())
        }
      }
      this.connection = this.form
      this.createConnection()
    },
    isActive(x, y) {
      return x == this.direction.x && y == this.direction.y
    },
    setActive(x, y) {
      this.direction.x = x
      this.direction.y = y
      this.updateDirection()
    },
    updateDirection() {
      let map = (value, x1, y1, x2, y2) => ((value - x1) * (y2 - x2)) / (y1 - x1) + x2

      let value = {
        x: map(this.direction.x, -1, 1, -1023, 1023),
        y: map(this.direction.y, -1, 1, 30, 180),
      }
      let publishMessage

      if (value.x !== this.value.x && value.y !== this.value.y) {
        publishMessage = `d${value.x},t${value.x}`
      } else if (value.x !== this.value.x) {
        publishMessage = `d${value.x}`
      } else if (value.y !== this.value.y) {
        publishMessage = `t${value.y}`
      }
      this.value = value

      this.publish.payload = publishMessage
      this.logger = publishMessage + '\n' + this.logger
      this.doPublish()

      this.scrollTop()
    },
    scrollTop() {
      let logger = document.getElementById('logger')
      logger.scrollTo({
        top: 0,
      })
    },
  },
  mounted() {
    this.$nextTick(function() {
      this.createConnection()
    })
  },
}
</script>

<style lang="scss">
body {
  background-color: #f0f2f5;
  padding: 0;
  margin: 0;
  color: rgba(0, 0, 0, 0.65);
  font-size: 14px;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif, Apple Color Emoji, Segoe UI Emoji,
    Segoe UI Symbol;
}

.home-container {
  max-width: 800px;
  margin: 0 auto;
  .el-card {
    margin: 8px;
    padding: 0;
  }
  .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    text-align: center;
  }

  #logger {
    padding: 1em 1em 10em 1em;
    line-height: 1em;
    overflow: hidden;
  }
}
</style>
