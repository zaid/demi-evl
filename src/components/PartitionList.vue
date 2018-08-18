<template>
  <article class="message">
    <div class="message-header">
      <p>Partitions</p>
    </div>
    <div class="message-body">
      <div class="field is-grouped is-grouped-multiline">
        <div v-for="partition in partitions" v-bind:key="partition.name" class="control">
          <div class="tags has-addons">
            <span class="tag is-primary">{{ partition.number }}</span>
            <span class="tag is-white">{{ partition.name }}</span>
          </div>
        </div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  name: 'partition-list',
  props: {
    partitions: {
      type: Array,
      default: function() {
        return []
      }
    }
  }
}
</script>
