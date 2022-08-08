<template lang="">
    <div class="select">
        <p
            class="title"
            @click="areOptionsVisible = !areOptionsVisible"
        >{{selected}}</p>
        <div
            class="options"
            v-if="areOptionsVisible"
        >
            <p
                v-for="option in options"
                :key="option.value"
                @click="selectOption(option)"
            >{{option.name}}</p>
        </div>
    </div>
</template>
<script>
export default {
    name: 'select-comp',
    props: {
        options: {
            type: Array,
            default() {
                return []
            }
        },
        selected: {
            type : String,
            default: ''
        }
    },
    data() {
        return {
            areOptionsVisible: false
        }
    },
    methods: {
        selectOption(option) {
            this.$emit('select', option)
            this.areOptionsVisible = false
        }
    },
}
</script>
<style>
.select {
    cursor: pointer;
    position: relative;
    width: 200px;
    background-color: #fff;
}

.select p {
    margin: 0;
}

.title {
    border: 1px solid #aeaeae;
}

.options {
    border: 1px solid #aeaeae;
    position: absolute;
    top: 20px;
    left: 0;
    width: 100%;
}
.options p:hover {
    background: #e7e7e7;
}
</style>