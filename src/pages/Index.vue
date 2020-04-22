<template>
  <q-page class='flex flex-center'>
    <q-layout>
      <q-toolbar>
        <q-toolbar-title :padding='1'>
          My Todo
        </q-toolbar-title>
        <button @click='add'>
          <i>add</i>
        </button>
      </q-toolbar>
      <q-list bordered padding v-if="items.length>0">
        <q-item v-for='(item, index) in items' :key='index'>
          <q-item-section>
            <span :class="item.completed ? 'completed-line' : ''">{{item.name}}</span>
          </q-item-section>
          <q-item-section avatar>
            <q-toggle class="item-secondary"
                      icon="done"
                      v-model="item.completed"
            ></q-toggle>
          </q-item-section>
        </q-item>
        <q-separator spaced />
      </q-list>
    </q-layout>
  </q-page>
</template>

<style>
.completed-line {
  text-decoration: line-through;
}
</style>

<script>

export default {
  name: 'PageIndex',
  data() {
    return {
      items: [],
    };
  },
  methods: {
    add() {
      this.$q.dialog({
        title: 'New task',
        prompt: {
          task: {
            type: 'textbox',
            model: '',
          },
        },
        cancel: true,
        persistent: true,
      })
        .onOk((newTask) => {
          this.items.push({
            name: newTask,
            completed: false,
          });
        });
    },
    remove() {

    },
  },
};
</script>
