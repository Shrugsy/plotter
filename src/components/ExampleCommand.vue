<template>
    <li>
        <button class="collapsible" v-on:click="toggleCollapse()" v-bind:class="{'active':!this.collapsed}">{{example.title}}</button>
        <div ref="myContent" class="content">
            <div v-for="(command, idx) in example.commands" :key="idx">{{command}}</div>
        </div>
    </li>
</template>

<script>
export default {
    name: "ExampleCommand",
    props: ["example"],
    data() {
        return {
            collapsed: true
        }
    },
    methods: {
        toggleCollapse(){
            let content = this.$refs.myContent;
            if (content.style.maxHeight){
                content.style.maxHeight = null;
            } else {
                content.style.maxHeight = content.scrollHeight + 'px';
            }
            this.collapsed = !this.collapsed;
        }
    }
}
</script>

<style scoped>
.collapsible {
    font-weight: bold;
    background-color: #777;
    color: white;
    cursor: pointer;
    padding: 9px;
    width: 100%;
    border: none;
    text-align: left;
    outline: none;
    font-size: 15px;
}

.collapsible:after {
    content: '\002B';
    color: white;
    font-weight: bold;
    float: right;
    margin-left: 5px;
}

.active:after {
    content: "\2212";
}

.active, .collapsible:hover {
    background-color: #555;
}

.content {
    padding: 0 18px;
    max-height: 0;
    overflow: hidden;
    transition: all 0.2s ease-in-out;
    background-color: #f1f1f1;
}
</style>