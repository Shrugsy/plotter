<template>
    <div class="coords">
        <svg>
            <Shape v-for="command in commands" v-bind:command="command" v-bind:key="command.idx">
            </Shape>
        </svg>
    </div>

</template>

<script>
import Shape from './Shape'

export default {
    name: "SVGOutput",
    components: {
        Shape
    },
    props: ["commands"]
}
</script>

<style scoped>
    svg {
        width: 250px;
        height: 250px;
        border: 1px solid black;
        background: white;
    }

    .coords::before {
        content: "0, 0";
        position: relative;
        top: -255px;
    }
    .coords::after {
        content: "250, 250";
        position: relative;
        top: 1.1em;
    }

</style>