<template>
  <form :class='classList' @submit.prevent='addList'>
    <!-- preventでサブミット時にリロードを防ぐ -->
    <input
      :value='title'
      @input="title = $event.target.value"
      type="text"
      class='text-input'
      placeholder="Add new List"
      @focusin='startEditing'
      @focusout='finishEditing'
    >
    <button type='submit' class='add-button'>
      Add
    </button>
  </form>
</template>

<script>
export default {
  data: function() {
    return {
      title: '',
      isEditing: false,
    }
  },
  computed: {
    classList() {
      const classList = ['addList']
      if(this.isEditing) {
        classList.push('active')
      }
      return classList
    },
  },
  methods: {
    addList: function() {
      this.$store.dispatch('addList', { title: this.title })
      this.title = ''
    },
    startEditing() {
      this.isEditing = true
    },
    finishEditing() {
      this.isEditing = false
    }
  }
}
</script>
