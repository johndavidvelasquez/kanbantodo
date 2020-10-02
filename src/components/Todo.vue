<template>
  <v-container fluid>
    <v-row align="center" justify="center" class="board">
      <!-- TODO -->
      <v-row>
        <v-col cols="6" md="4" ma="6">
          <v-card class="mx-auto" min-width="400">
            <v-card-title id="cardTodoTitle">
              <v-icon color="white">mdi-message-text</v-icon>Todo
            </v-card-title>
            <v-list>
              <draggable class="list-group" :list="todo" group="tasks">
                <v-list-item
                  class="list-group-item"
                  v-for="(element, index) in todo"
                  :key="index"
                >
                  <v-card class="itemCard">
                    <v-card-title class="itemCardTitleTodo">
                      <v-list-item-title
                        v-html="element.name"
                      ></v-list-item-title>
                    </v-card-title>
                    <v-card-actions>
                      <div class="actions-container">
                        <v-btn class="mx-2" x-small top right fab>
                          <v-icon dark> mdi-pencil </v-icon>
                        </v-btn>
                        <v-btn class="mx-2" x-small top right fab>
                          <v-icon dark> mdi-delete-empty </v-icon>
                        </v-btn>
                      </div>
                    </v-card-actions>
                  </v-card>
                </v-list-item>
              </draggable>
            </v-list>
            <v-card-actions>
              <v-dialog v-model="dialog" persistent max-width="600px">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn color="primary" dark v-bind="attrs" v-on="on">
                    ADD
                  </v-btn>
                </template>
                <v-card>
                  <v-card-title>
                    <span class="headline">Add Task</span>
                  </v-card-title>
                  <v-card-text>
                    <v-container>
                      <v-row>
                        <v-col cols="12">
                          <v-text-field
                            ref="task"
                            label="Task"
                            v-model="newtask"
                            :rules="[
                              () => !!newtask || 'This field is required',
                            ]"
                            required
                          ></v-text-field>
                        </v-col>
                      </v-row>
                    </v-container>
                    <small>*indicates required field {{ newtask }}</small>
                  </v-card-text>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue darken-1" text @click="dialog = false"
                      >Close</v-btn
                    >
                    <v-btn color="blue darken-1" type="submit" @click="add"
                      >Save</v-btn
                    >
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
      <!-- INPROGRESS -->
      <v-row>
        <v-col cols="6" md="4" ma="6">
          <v-card class="mx-auto" min-width="400">
            <v-card-title id="cardInProgressTitle">
              <v-icon color="white">mdi-progress-check</v-icon>IN PROGRESS
            </v-card-title>
            <v-list>
              <draggable class="list-group" :list="inprogress" group="tasks">
                <v-list-item
                  class="list-group-item"
                  v-for="(element, index) in inprogress"
                  :key="index"
                >
                  <v-card class="itemCard">
                    <v-card-title class="itemCardTitleInProgress">
                      <v-list-item-title
                        v-html="element.name"
                      ></v-list-item-title>
                    </v-card-title>
                    <v-card-actions>
                      <div class="actions-container">
                        <v-btn class="mx-2" x-small top right fab>
                          <v-icon dark> mdi-pencil </v-icon>
                        </v-btn>
                        <v-btn class="mx-2" x-small top right fab>
                          <v-icon dark> mdi-delete-empty </v-icon>
                        </v-btn>
                      </div>
                    </v-card-actions>
                  </v-card>
                </v-list-item>
              </draggable>
            </v-list>
          </v-card>
        </v-col>
      </v-row>

      <!-- COMPLETED -->
      <v-row>
        <v-col cols="6" md="4" ma="6">
          <v-card class="mx-auto" min-width="400">
            <v-card-title id="cardCompletedTitle">
              <v-icon color="white">mdi-check</v-icon>COMPLETED
            </v-card-title>
            <v-list>
              <draggable class="list-group" :list="completed" group="tasks">
                <v-list-item
                  class="list-group-item"
                  v-for="(element, index) in completed"
                  :key="index"
                >
                  <v-card class="itemCard">
                    <v-card-title class="itemCardTitleCompleted">
                      <v-list-item-title
                        v-html="element.name"
                      ></v-list-item-title>
                    </v-card-title>
                    <v-card-actions>
                      <div class="actions-container">
                        <v-btn class="mx-2" x-small top right fab>
                          <v-icon dark> mdi-pencil </v-icon>
                        </v-btn>
                        <v-btn class="mx-2" x-small top right fab>
                          <v-icon dark> mdi-delete-empty </v-icon>
                        </v-btn>
                      </div>
                    </v-card-actions>
                  </v-card>
                </v-list-item>
              </draggable>
            </v-list>
          </v-card>
        </v-col>
      </v-row>
    </v-row>
  </v-container>
</template>

<script>
import draggable from "vuedraggable";
export default {
  name: "Todo",

  components: {
    draggable,
  },

  data: () => ({
    dialog: false,
    newtask: "",
    todo: [
      { name: "John", id: 1 },
      { name: "Joao", id: 2 },
      { name: "Jean", id: 3 },
      { name: "Gerard", id: 4 },
    ],
    inprogress: [
      // { name: "Juan", id: 5 },
      // { name: "Edgard", id: 6 },
      // { name: "Johnson", id: 7 }
    ],
    completed: [
      // { name: "Juan", id: 5 },
      // { name: "Edgard", id: 6 },
      // { name: "Johnson", id: 7 }
    ],
  }),
  methods: {
    add: function () {
      if (this.newtask != "") {
        this.todo.push({
          name: this.newtask,
          id: this.todo.length + this.inprogress.length,
        });
        console.log(this.newtask);
        this.dialog = false;
        this.newtask = "";
      } else {
        this.newtask.validate(true);
      }
    },
  },
};
</script>

<style scoped>
.board {
  padding: 25px 5%;
}
.itemCard {
  width: 100%;
  margin-bottom: 5%;
}
#cardTodoTitle {
  background-color: #9c27b0;
  color: white;
}
.itemCardTitleTodo {
  border-top: 5px solid #9c27b0;
}
#cardInProgressTitle {
  background-color: #FFC107;
  color: white;
}
.itemCardTitleInProgress {
  border-top: 5px solid#FFC107;
}
#cardCompletedTitle {
  background-color: #4CAF50;
  color: white;
}
.itemCardTitleCompleted {
  border-top: 5px solid#4CAF50;
}
.actions-container {
  padding-left: 70%;
  padding-bottom: 3%;
}
</style>