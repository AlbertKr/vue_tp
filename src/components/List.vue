<template>
  <div class="list" @dragover.prevent @drop="onDrop(name)">
    <h1 class="list-name">{{ name }} {{ cards | countDone }}</h1>
    <div v-if="cards.length > 0" class="list-cards">
      <Card
      :onDrag="handleDrag(card)" v-for="card in cards" v-bind="card" v-bind:key="card.id" />
    </div>
    <div v-else>
      <p>Pas de cards</p>
    </div>
    <a @click="toggleForm"> + Add new card</a>
    <NewCard :open="showForm" :onClose="toggleForm" @new-card="handleNewCard" />
  </div>
</template>

<script>
import Card from './Card.vue'
import NewCard from './NewCardPlusPlus.vue'

export default {
  name: 'List',
  components: {
    Card,
    NewCard
  },
  props: {
    cards: Array,
    name: String,
    onNewCard: Function
  },
  data: () => ({
    draggedItem: null,
    showForm: false
  }),
  filters: {
    countDone: cards => cards.filter(card => card.status === "done").length
  },
  inject: ["onDrag", "onDrop"],
  methods: {
    toggleForm: function() {
      this.showForm = !this.showForm;
    },
    handleNewCard: function(card) {
      const { onNewCard, ...list } = this.$props;
      onNewCard && onNewCard;
      this.toggleForm();
      onNewCard(card, list);
    },
    handleDrag: function(card){
      const { onNewCard, ...list } = this.$props;
      onNewCard && onNewCard;
      return () => this.onDrag(card, list);
    },
    // onDrag: function(card, list) {
    //   this.draggedItem = {
    //     card,
    //     list
    //   };
    // }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  div.list {
    height: 100%;
    max-height: 100%;
    display: flex;
    overflow-y: scroll;
    flex-direction: column;
    flex: 1;
    width: 20%;
    background-color: blue;
    margin-left: 10px;
    overflow-x: hidden;
  }
  div.list-name {
    background-color: white;
  }
  div.list-cards {
    flex: 1;
    background-color: aquamarine;
  }
</style>