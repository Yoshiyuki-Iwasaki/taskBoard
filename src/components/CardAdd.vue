<template>
  <form :class="classList" @submit.prevent="addCardToList">
    <input v-model="body"
           type="text"
           class="text-input"
           placeholder="Add new card"
           @focusin="startEditing"
           @focusout="finishEditing"
    />
    <button type="submit"
            class="add-button"
            v-if="isEditing || bodyExists">
      Add
    </button>
  </form>
</template>

<script>
export default {
  props: {
    listIndex: {
      type: Number,
      required: true
    }
  },
  data: function() {
    return {
      body: '',
      isEditing: false,
    }
  },
  computed: {
    classList() {
      const classList = ['addcard']
      if(this.isEditing) {
        classList.push('active')
      }
      if(this.bodyExists) {
        classList.push('addable')
      }
      return classList;
    },
    bodyExists() {
      return this.body.length > 0
    }
  },
  methods: {
    startEditing: function() {
      this.isEditing = true
    },
    finishEditing: function() {
      this.isEditing = false
    },
    addCardToList: function() {
      this.$store.dispatch('addCardToList', { body: this.body, listIndex: this.listIndex })
      this.body = ''
    }
  }
}
</script>

<style scoped>
  .text-input {
    padding: 15px;
    width: calc(100% - 30px);
    background-color: #ccc;
    border-radius: 8px;
    cursor: pointer;
    border: none;
    font-weight: 700;
    font-size: 18px;
    color: #242424;
    overflow: overlay;
  }
  
  .text-input:focus {
    outline: 0;
    cursor: initial;
  }
  
  .add-button {
    margin-top: 15px;
    padding: 15px 18px;
    background-color: #999;
    border: none;
    border-radius: 8px;
    font-weight: 700;
    font-size: 18px;
    color: #fff;
  }
  
  .add-button:hover {
    opacity: 0.8;
    cursor: pointer;
  }
  
  .active .text-input {
    background-color: #fff;
  }
  .addable .add-button {
    background-color: #00d78f;
    pointer-events: auto;
    cursor: pointer;
  }
  
  .add-button:active {
    background-color: #00d78f;
  }
  
  .list {
    margin: 0 5px auto;
    position: relative;
    display: inline-block;
    flex-direction: column;
    align-items: flex-start;
    min-width: 290px;
    width: 290px;
    background-color: #e0e0e0;
    border-radius: 8px;
    padding: 15px;
    border: solid #ddd 1px;
    color: gray;
    vertical-align: top;
  }
  
  .deletelist {
    position: absolute;
    top: 6px;
    right: 14px;
    font-size: 28px;
  }
  
  .deletelist:hover {
    opacity: 0.8;
    cursor: pointer;
  }
  
  .close-button {
    position: absolute;
    top: 6px;
    right: 15px;
    font-size: 22px;
    cursor: pointer;
    border-radius: 8px;
    border-color: red;
    border-style: solid;
    background-color: red;
    color: white;
    margin: 5px;
  }
  
  .body {
    font-size: 18px;
    width: 100%;
    word-wrap: break-word;
  }

  .addcard {
    margin-top: 10px;
  }
</style>