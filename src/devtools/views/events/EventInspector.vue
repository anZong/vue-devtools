<template>
  <scroll-pane>
    <div v-if="activeEvent" slot="scroll" class="data-fields">
      <data-field v-for="(value, key) of sortedEventData"
        :field="{ key, value }"
        :depth="0">
      </data-field>
    </div>
    <div v-else slot="scroll" class="no-event-data">
      No event selected
    </div>
  </scroll-pane>
</template>

<script>
import DataField from 'components/DataField.vue'
import ScrollPane from 'components/ScrollPane.vue'
import ActionHeader from 'components/ActionHeader.vue'

import { mapGetters } from 'vuex'

export default {
  components: {
    DataField,
    ScrollPane,
    ActionHeader
  },
  computed: {
    ...mapGetters('events', [
      'activeEvent'
    ]),
    sortedEventData () {
      if (!this.activeEvent) {
        return {}
      }
      return {
        name: this.activeEvent.eventName,
        type: this.activeEvent.type,
        source: '<' + this.activeEvent.instanceName + '>',
        payload: this.activeEvent.payload
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
@import "../../common"

section:not(:last-child)
  border-bottom 1px solid $border-color
  .app.dark &
    border-bottom 1px solid $dark-border-color

.component-name
  margin 0 10px

.string
  color: #c41a16

.literal
  color: #03c

.no-event-data
  color: #ccc;
  text-align: center;
  margin-top: 50px;
  line-height: 30px;
</style>
