<template>
  <article class="message">
    <div class="message-header">
      <p>EvlDaemon Configuration</p>
    </div>
    <div class="message-body">
      <div class="columns">
        <div class="column"><strong>Storage Engines: </strong>{{ storageEngines }}</div>
      </div>
      <div class="columns">
        <div class="column"><strong>Listeners: </strong>{{ listeners }}</div>
      </div>
      <div class="columns">
        <div class="column"><strong>Notifiers: </strong>{{ notifiers }}</div>
      </div>
      <div class="columns">
        <div class="column"><strong>Tasks: </strong>{{ tasks }}</div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  name: 'evl-daemon-config',
  props: {
    config: {
      type: Object,
      default: function() {
        return { storage: '', listeners: '', notifiers: '', tasks: '' }
      }
    }
  },
  computed: {
    storageEngines: function() {
      return this.config.storage.join(", ")
    },
    listeners: function() {
      return this.config.listeners.join(", ")
    },
    notifiers: function() {
      return this.config.notifiers.join(", ")
    },
    tasks: function() {
      return this.config.tasks.join(", ")
    }
  }
}
</script>
