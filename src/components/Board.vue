<template>
  <div>
    <header>
      my Trello
    </header>
    <main>
      <p class='info-line'>All: {{ totalTasks }} tasks</p>
        <div>
          <draggable :list='lists' @end='movingList' class='list-index'>
            <list
              v-for='(item, index) in lists'
              :key='item.id'
              :title='item.title'
              :cards='item.cards'
              :listIndex='index'
              @change='movingCard'
            />
            <list-add />
          </draggable>
        </div>
    </main>
  </div>
</template>

<script>
import ListAdd from './ListAdd'
import List from './List'
import draggable from 'vuedraggable'
import { mapState } from 'vuex'

export default {
  components: {
    ListAdd,
    List,
    draggable
  },
  computed: {
    // 以下は繰り返し書いたら冗長になる
    // lists: function() {
    //   return this.$store.state.lists
    // }
    // スプレッド演算子をつけることで、外のオブジェクトとこのオブジェクトを混ぜている
    // ネストされたオブジェクトを渡してはいけない
    ...mapState([
      'lists'
    ]),
    totalTasks: function(){
      return this.$store.getters.totalTasks
    }
  },
  methods: {
    movingCard: function() {
      this.$store.dispatch('updateList', { lists: this.lists })
    },
    movingList: function() {
      this.$store.dispatch('updateList', { lists: this.lists })
    }
  }
}
</script>