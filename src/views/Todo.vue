<template>
  <div class="todo">
    <v-text-field
            outlined
            hide-details
            clearable
            v-model="taskTitle"
            class="pa-3 pb-1"
            label="Add Task"
            append-icon="mdi-plus"
            @click:append="addTask()"
            @keyup.enter="addTask()"
          ></v-text-field>
    <v-list flat>
      <v-list-item-group v-model="settings" multiple>
        <div v-for="task in tasks" :key="task.id">
          <v-list-item :class="{'green lighten-3': task.done}" @click="task.done = !task.done">
            <template>
              <v-list-item-action>
                <v-checkbox :input-value="task.done" color="green darken-3"></v-checkbox>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title :class="{'text-decoration-line-through': task.done}" v-text="task.title"></v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn icon @click.stop="deleteTask(task.id)">
                  <v-icon color="red lighten-1">mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </template>
          </v-list-item>
          <v-divider></v-divider>
        </div>
      </v-list-item-group>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data: function() {
    return {
      settings: [],
      taskTitle: ``,
      tasks: [
        {
          id: 1,
          title: "Wake Up",
          done: false,
        },
        {
          id: 2,
          title: "Go To Pray",
          done: false,
        },
        {
          id: 3,
          title: "GO to Eating",
          done: false,
        },
      ],
    };
  },
  methods: {
    addTask: function () {

      if (this.taskTitle.trim() === '') {
        return this.taskTitle = '';
      }
      let newTask = {
        id: Date.now(),
        title: this.taskTitle,
        done: false,
      }
      this.tasks.push(newTask);
      this.taskTitle = "";
    },
    deleteTask: function (id) {
      this.tasks = this.tasks.filter(item => item.id !== id);
    },
  },
};
</script>
