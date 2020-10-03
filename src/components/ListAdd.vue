<template>
    <form :class="classList" @submit.prevent="addList">
        <input v-model="title"
                type="text"
                class="text-input"
                placeholder="Add new list"
                @focusin="startEditing"
                @focusout="finishEditing"
        >
        <button type="submit" 
                class="add-button"
                v-if="isEditing || titleExists">
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
    methods:{
        addList: function() {
            this.$store.dispatch('addlist', {title: this.title})
            this.title = ''
        },
        startEditing: function() {
            this.isEditing = true;
        },
        finishEditing: function() {
            this.isEditing = true;
        }
    },
    computed: {
        classList() {
            const classList = ['addList']
            if(this.isEditing) {
                classList.push('active')
            }
            if(this.titleExists) {
                classList.push('addable')
            }
            return classList
        },
        titleExists() {
            return this.title.length > 0
        }
    },
}
</script>

<style scoped>
  .addlist {
    margin: 0 10px auto;
    display: inline-block;
    flex-direction: column;
    align-items: flex-start;
    min-width: 320px;
    width: 320px;
  }
  
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
</style>