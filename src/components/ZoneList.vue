<template>
  <article class="message">
    <div class="message-header">
      <p>Zones</p>
    </div>
    <div class="message-body">
      <div class="field is-grouped is-grouped-multiline">
        <div v-for="zone in zones" v-bind:key="zone.name" class="control">
          <div class="tags has-addons">
            <span class="tag is-primary">{{ zone.number }}</span>
            <span class="tag is-white">{{ zone.name }}</span>
          </div>
        </div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  name: 'zone-list',
  props: {
    zones: {
      type: Array,
      default: function() {
        return []
      }
    }
  }
}
</script>
