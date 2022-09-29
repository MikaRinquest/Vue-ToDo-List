<template>
  <div>
    <v-text-field
      v-model="newTaskTitle"
      class="pa-3"
      outlined
      label="Add new task"
      hide-details
      clearable
      append-outer-icon="mdi-plus-circle"
      @click:append-outer="addNewTask"
      @keyup.enter="addNewTask"
    ></v-text-field>
    <v-list class="pt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'purple lighten-3': task.status }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.status"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.status }"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color="grey darken-4">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTaskTitle: "",
      tasks: [
        {
          id: 1,
          title: "Wake Up",
          status: false,
        },
        {
          id: 2,
          title: "Go to bathroom",
          status: false,
        },
        {
          id: 3,
          title: "Brush Teeth",
          status: false,
        },
      ],
    };
  },
  methods: {
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.status = !task.status;
      //This function makes it so that whenever you click on the task and not just the checkbox, it registers the task as done/undone
    },

    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
      // Just creates a new array without the object with an id similiar to the object that we clicked on's id
    },

    addNewTask() {
      const task = {
        id: Date.now,
        title: this.newTaskTitle,
        done: false,
      };
      this.tasks.push(task);
      this.newTaskTitle = "";
    },
  },
};
</script>
