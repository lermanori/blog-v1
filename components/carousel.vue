<template>
  <v-container
    fluid
    class="px-0"
    v-touch="{
      left: () => swipeLeft(),
      right: () => swipeRight(),
    }"
  >
    <transition :enter-active-class="enter_class" :leave-active-class="leave_class" mode="out-in">
      <app-item
        :color="arr[Index].color"
        :key="arr[Index].color"
        :name="arr[Index].name"
        :body="arr[Index].body"
        :issue="arr[Index].issue"
        :src="arr[Index].src"
        :buttons="Math.min(arr.length,3)"
        @oldest="changeIndex(arr.length -3 )"
        @mid="changeIndex(arr.length -2 )"
        @new="changeIndex(arr.length -1 )"
        :index="Index"
      />
    </transition>
  </v-container>
</template>

<script>
import item from "../components/item.vue";
export default {
  data: function() {
    return {
      transitions: {
        enter_class_left: "animated fadeInLeft",
        enter_class_right: "animated fadeInRight",
        leave_class_left: "animated fadeOutLeft",
        leave_class_right: "animated fadeOutRight"
      },
      enter_active_class: "animated fadeInLeft",
      leave_active_class: "animated fadeOutLeft",

      index: 1
    };
  },
  props: ["arr"],
  computed: {
    Index: function() {
      return this.index;
    },
    leave_class: function() {
      return this.leave_active_class;
    },
    enter_class: function() {
      return this.enter_active_class;
    }
  },
  methods: {
    changeIndex(arg) {
      this.index = arg;
    },
    swipeLeft() {
      this.enter_active_class = this.transitions.enter_class_left;
      this.leave_active_class = this.transitions.leave_class_left;
      this.changeIndex((this.Index - 1) % this.arr.length);
    },
    swipeRight() {
      this.enter_active_class = this.transitions.enter_class_right;
      this.leave_active_class = this.transitions.leave_class_right;
      this.changeIndex((this.Index + 1) % this.arr.length);
    }
  },
  components: { "app-item": item }
};
</script>

<style>
</style>
