<template>
  <div class="dashboard container">
    <system-status v-bind:state="state" />

    <div class="tile is-ancestor">
      <div class="tile is-parent is-2">
        <div class="tile is-child">
          <partition-list v-bind:partitions="partitions" />
        </div>
      </div>
      <div class="tile is-parent is-3">
        <div class="tile is-child">
          <zone-list v-bind:zones="zones" />
        </div>
      </div>
      <div class="tile is-vertical is-parent is-5">
        <div class="tile is-child">
          <evl-module v-bind:connection="connection" />
        </div>
        <div class="tile is-child">
          <evl-daemon-config v-bind:config="configuration" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import EvlModule from './EvlModule.vue'
import EvlDaemonConfig from './EvlDaemonConfig.vue'
import ZoneList from './ZoneList.vue'
import PartitionList from './PartitionList.vue'
import SystemStatus from './SystemStatus.vue'

export default {
  name: 'Dashboard',
  components: {
    'evl-module': EvlModule,
    'evl-daemon-config': EvlDaemonConfig,
    'zone-list': ZoneList,
    'partition-list': PartitionList,
    'system-status': SystemStatus
  },
  data: function() {
    return {
      state: {}
    }
  },
  mounted: function() {
    this.queryDaemon()
  },
  methods: {
    queryDaemon: function() {
      fetch(
        'http://localhost:4000/system_status?auth_token=SECRET', { method: 'GET', headers: new Headers({ 'Content-Type': 'application/json' })}
      ).then(function(raw_data) {
        return raw_data.json()
      }).then(json => {
        this.state = json
      }).catch(function(error) {
        this.console.log('queryDaemon error: ' + error)
      })
    }
  },
  computed: {
    connection: function() {
      return this.state.connection
    },
    configuration: function() {
      return {
        storage: this.state.storage || [],
        notifiers: this.state.notifiers || [],
        listeners: this.state.listeners || [],
        tasks: this.state.tasks || []
      }
    },
    zones: function() {
      return this.state.zones
    },
    partitions: function() {
      return this.state.partitions
    },
  }
}
</script>

<style lang="css">
  div.dashboard {
    padding-top: 3em;
  }
</style>
