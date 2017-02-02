<style>
.block {
    position: relative;
    width: 20%;
    height: 25%;
    background: #efefef;
    color: #fff;
    float: left;
    box-sizing: border-box;
    -moz-box-sizing: border-box;
    /* Firefox */
    -webkit-box-sizing: border-box;
    /* Safari */
    padding: 20px;
    cursor: pointer;
}

.block .name {
    text-transform: uppercase;
    position: absolute;
    right: 10px;
    bottom: 10px;
}

.block .hover {
    text-transform: uppercase;
    position: absolute;
    padding: 2% 10%;
    border: 2px solid rgba(255, 255, 255, .3);
    border-radius: 4px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    opacity: 0;
    transition: opacity .25s ease-in-out;
    -moz-transition: opacity .25s ease-in-out;
    -webkit-transition: opacity .25s ease-in-out;
}

.hover {
    transition: opacity .25s ease-in-out;
    -moz-transition: opacity .25s ease-in-out;
    -webkit-transition: opacity .25s ease-in-out;
    opacity: 0;
    display: block;
}

.block:hover .hover {
    opacity: 1;
}

.block .hex {
    position: absolute;
    right: 20px;
    bottom: 20px;
}

.visible {
    visibility: visible;
    opacity: 1;
    transition: opacity 2s linear;
}

.hidden {
    visibility: hidden;
    opacity: 0;
    transition: visibility 0s 2s, opacity 2s linear;
}
</style>

<template>
<div class="block" v-on:click="notify_copy" :style="{ background: block.hex }" v-bind:id="block.name" v-bind:rgb="rgb" v-bind:hex="block.hex">
    <span class="name">{{block.name}}</span>
    <div class="hover">Copy</div>
</div>
</template>

<script>
export default {
    props: ['block', 'index', 'id'],
    name: 'block',
    data() {
        return {
            hex: this.hex,
        }
    },
    /**
     * Event triggers method on parent object
     */
    methods: {
        notify_copy: function() {
            if (this.$parent.selected == 'hex') {
                this.$parent.$emit('copy', this.block.hex);
            } else {
                this.$parent.$emit('copy', this.block.rgb);
            }
        }
    },
    computed: {
        rgb: function() {
            var hex = this.block.hex.replace(/\#/g, '0x');
            var r = hex >> 16;
            var g = hex >> 8 & 0xFF;
            var b = hex & 0xFF;
            this.block.rgb = 'rgb(' + r + ' , ' + g + ' , ' + b + ')';
            return [r, g, b];
        }
    }
}
</script>
