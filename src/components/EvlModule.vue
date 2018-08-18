<template>
  <article class="message">
    <div class="message-header">
      <p>EVL Module</p>
    </div>
    <div class="message-body">
      <div class="columns">
        <div class="column"><strong>Host:</strong>{{ host }}</div>
        <div class="column"><strong>Port:</strong>{{ port }}</div>
        <div class="column"><strong>Connected:</strong> {{ connected }}</div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  name: 'evl-module',
  props: {
    connection: {
      type: Object,
      default: function() {
        return {}
      }
    }
  },
  computed: {
    host: function() {
      return this.connection["host"]
    },
    port: function() {
      return this.connection["port"]
    },
    connected: function() {
      return this.connection["alive?"]
    }
  }
}
</script>
