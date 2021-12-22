<template>
  <div>
    <a-button type="primary" @click="onClick">
      {{clicked ? 'CLICK ME HARDER' : 'CLICK ME'}} {{ reversedMessage }}
    </a-button>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      clicked: false,
    }
  },
  methods: {
    onClick() {
      this.clicked = !this.clicked;
    }
  },
}
</script>
