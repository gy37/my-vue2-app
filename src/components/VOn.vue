<template>
  <div>
    <button v-on:click="greet">Greet</button>
    <button v-on:click="warn('Form cannot be submitted yet.', $event)">Submit</button>
  </div>
</template>

<script>
export default {
  name: 'VOn',
  data: function () {
    return {
      name: 'VOn.vue',
    }
  },
  methods: {
    greet: function (event) {
      alert('Hello ' + this.name + '!');
      if (event) {
        alert(event.target.tagName)
      }
    },
    warn: function (message, event) {
      if (event) {
        event.preventDefault();
      }
      alert(message);
    }
  }
}
</script>

<style lang="scss" scoped></style>