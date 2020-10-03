<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <p class="list-counter">total: {{ totalCardInList }}</p>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <draggable class="cardGroup" group="cards"
           :list="cards"
           @end="$emit('change')">
        <card v-for="(item, index) in cards"
                :body="item.body"
                :key="item.id"
                :cardIndex="index"
                :listIndex="listIndex"
        />
        <card-add :listIndex="listIndex"/>
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
    totalCardInList() {
        return this.cards.length
    }
  },
  methods: {
    removeList: function() {
      if(confirm('本当にこのリストを削除しますか？')) {
        this.$store.dispatch('removelist', { listIndex: this.listIndex })
      }
    },
  }
}
</script>

<style scoped>
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
  
  .listheader {
    margin-top: 20px;
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
  }
  
  .list-title {
    font-size: 22px;
    font-weight: bold;
  }
  
  .list-counter {
    font-size: 15px;
    color: #242424;
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

  .cardGroup {
    margin-top: 15px;
  }
</style>