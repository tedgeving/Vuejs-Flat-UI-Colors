<style>
.toggle select {
    margin: 0 auto;
    display: block;
}

.center {
    text-align: center;
}
</style>

<template id="toggle">
<div class="toggle">
    <h3 class="center">Color Format</h3>
    <select v-model="selected" v-on:change="notify_selection">
        <option v-for="option in options" :value="option">{{ option }}</option>
    </select>
</div>
</template>

<script>
export default {
    name: 'toggle',
    props: ['options', 'init'],
    data() {
        return {
            selected: 'hex'
        }
    },
    methods: {
        notify_selection: function() {
            this.$parent.$emit('update', this.selected); //HACKish
        }
    }
}
</script>
