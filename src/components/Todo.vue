<template>
  <v-container fluid>
    <v-row align="center" justify="center">
      <v-card
        class="mx-auto"
        max-width="344"
        outlined
      >
        <v-list-item>
          <v-list-item-content>
            <div class="overline mb-3">TODO</div>
            <v-list-item-title class="headline mb-1">Headline 5</v-list-item-title>
            <v-list-item-subtitle>Greyhound divisely hello coldly fonwderfully</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <div>
            <draggable class="list-group" :list="todo" group="people">
              <div
                class="list-group-item"
                v-for="(element, index) in todo"
                :key="element.name"
              >
                 <v-chip class="ma-2" label>{{ element.name }} {{ index }}</v-chip>
              </div>
            </draggable>
        </div>

        <v-card-actions>
          <v-btn text>Add</v-btn>
        </v-card-actions>
      </v-card>
    </v-row>

    
  </v-container>
</template>

<script>
import draggable from "vuedraggable";

  export default {
    name: 'Todo',

    components: {
      draggable
    },

    data: () => ({
       todo: [
        { name: "John", id: 1 },
        { name: "Joao", id: 2 },
        { name: "Jean", id: 3 },
        { name: "Gerard", id: 4 }
      ],
      list2: [
        { name: "Juan", id: 5 },
        { name: "Edgard", id: 6 },
        { name: "Johnson", id: 7 }
      ]
    }),
  }
</script>
