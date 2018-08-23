<template>
  <div class="box">
    <div class="columns">
      <div class="column is-10">
        <div class="field is-grouped">
          <span><strong>System Status:</strong>&nbsp;</span>
          <div v-for="armedPartition in armed_state" v-bind:key="armedPartition.number" class="control">
            <div class="tags has-addons">
              <span v-bind:class="armed_class(armedPartition)">{{ armedPartition.partition }}</span>
              <span class="tag">{{ armedPartition.state }}</span>
            </div>
          </div>
        </div>
        <p>
          <strong>Latest Event:</strong>&nbsp;
          {{ latest_event }}
        </p>
      </div>
      <div class="column">
        <p><Strong>Uptime: </strong>{{ uptime }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'system-status',
  props: {
    state: {
      type: Object,
      default: function() {
        return {
          armed_state: {}, uptime: 0, last_event: {}
        }
      }
    }
  },
  computed: {
    armed_state: function() {
      return this.state.armed_state
    },
    uptime: function() {
      var uptimeInSeconds = this.state.uptime

      if (uptimeInSeconds < 60)
        return (uptimeInSeconds + " seconds.")
      else if (uptimeInSeconds > 60 && uptimeInSeconds < 3600)
        return this.roundToTwoDecimals(uptimeInSeconds / 60) + " minutes."
      else if (uptimeInSeconds > 3600 && uptimeInSeconds < 86400)
        return this.roundToTwoDecimals(uptimeInSeconds / 3600) + " hours."
      else
        return this.roundToTwoDecimals(uptimeInSeconds / 86400) + " days."
    },
    latest_event: function() {
      var nuggets = [this.state.last_event.description.data, this.state.last_event.description.command]

      return nuggets.filter(function(nugget) { return nugget != null }).join(' - ')
    }
  },
  methods: {
    roundToTwoDecimals: function(number) {
      return Math.round(number * 10) / 10
    },
    armed_class: function(armed_partition) {
      return {
        tag: true,
        'is-primary': armed_partition.state === 'Unarmed.',
        'is-warning': armed_partition.state === 'Failed to arm.',
        'is-success': armed_partition.state.match(/^Armed in /)
      }
    }
  }
}
</script>
