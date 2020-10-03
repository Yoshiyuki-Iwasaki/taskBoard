<template>
  <div class="Board">
    <Header></Header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <div class="list-index">
        <draggable :list="lists"
                    @end="movingList"
                    class="list-index">
          <list v-for="(item, index) in lists"
                :key="item.id"
                :title="item.title"
                :cards="item.cards"
                :listIndex="index"
                @change="movingCard"
          />
          <list-add/>
        </draggable>
      </div>
    </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import List from './List'
import ListAdd from './ListAdd'
import Header from './Header'
import { mapState } from 'vuex'

export default {
  components: {
    draggable,
    ListAdd,
    List,
    Header,
  },
  computed: {
    ...mapState([
      'lists'
    ]),
    totalCardCount() {
      return this.$store.getters.totalCardCount
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

<style scoped>
  main {
    padding: 0 10px;
    width: calc(100% - 40px);
    height: 100%;
  }
  
  .info-line {
    margin: 20px;
    font-size: 20px;
    color: #fff;
    font-weight: 500;
  }
  
  .list-index {
    display: flex;
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