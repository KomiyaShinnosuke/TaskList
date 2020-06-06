<template>
  <div class='list'>
    <div class='listheader'>
      <p class='list-title'>{{ title }}</p>
      <p class='list-counter'>total: {{ totalCardInList }}</p>
      <div class='deletelist' @click='removeList'>x</div>
    </div>
    <draggable group='cards' :list='cards' @end="$emit('change')">
      <card
        v-for='(item, index) in cards'
        :key='item.id'
        :body='item.body'
        :listIndex='listIndex'
        :cardIndex='index'
      />
      <card-add :listIndex='listIndex' />
    </draggable>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import CardAdd from './CardAdd'
import Card from './Card'

export default {
  components: {
    CardAdd,
    Card,
    draggable
  },
  props: {
    title: {
      type: String,
      required: true
    },
    cards: {
      type: Array,
      required: true
    },
    listIndex: {
      type: Number,
      required: true
    }
  },
  computed: {
    totalCardInList: function() {
      return this.cards.length
    }
  },
  methods: {
    removeList: function() {
      if(confirm('really remove this list?')){
        this.$store.dispatch('removeList', { listIndex: this.listIndex })
      }
    }
  }
}
</script>