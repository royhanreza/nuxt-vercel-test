<template>
    <div>
        <button @click="decrease">-</button>
        <span>{{ number }}</span>
        <button @click="increase">+</button>
    </div>
</template>
<script>
export default {
    name: 'CounterContainer',
    data() {
        return {
            number: 0,
        }
    },
    methods: {
        decrease() {
            const self = this;
            self.number--;
        },
        increase() {
            const self = this;
            self.number++;
        }
    }
}
</script>

<style>

</style>