<template>
    <div class="card">
        <button class="close-button" @click="removeCardFromList">x</button>
        <div class="body">
            {{ body }}
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            body: {
                type: String,
                required: true
            },
            listIndex: {
                type: Number,
                required: true
            },
            cardIndex: {
                type: Number,
                required: true
            }
        },
        methods: {
            removeCardFromList: function() {
                if(confirm('本当にこのカードを削除しますか？')) {
                    this.$store.dispatch('removeCardFromList', { cardIndex: this.cardIndex, listIndex: this.listIndex })
                }
            }
        },
    }
</script>

<style scoped>
  .card {
    margin-top: 10px;
    position: relative;
    display: flex;
    padding: 25px 15px;
    background-color: #fff;
    border-radius: 8px;
    width: 260px;
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
</style>