<template>

  <rect
    class="shape"
    v-if="command[0] == 'R'"
    v-bind:x="command[1]"
    v-bind:y="command[2]"
    v-bind:width="command[3]"
    v-bind:height="command[4]"
    v-bind:fill="getRandomColor()"
  />
  <circle
    class="shape"
    v-else-if="command[0] == 'C'"
    v-bind:cx="command[1]"
    v-bind:cy="command[2]"
    v-bind:r="command[3]"
    v-bind:fill="getRandomColor()"
  />
  <polygon
    class="shape"
    v-else-if="command[0] == 'P'"
    v-bind:points="command[1]"
    v-bind:fill="getRandomColor()"
  />
  <ellipse 
    class="shape"
    v-else-if="command[0] == 'E'"
    v-bind:cx="command[1]"
    v-bind:cy="command[2]"
    v-bind:rx="command[3]"
    v-bind:ry="command[4]"
    v-bind:fill="getRandomColor()"
  />
  <line 
    class="shape"
    v-else-if="command[0] == 'L'"
    v-bind:x1="command[1]"
    v-bind:y1="command[2]"
    v-bind:x2="command[3]"
    v-bind:y2="command[4]"
    v-bind:style="`stroke:${getRandomColor()};stroke-width:${command[5]}`"
  />
  <polyline 
    class="shape"
    v-else-if="command[0] == 'PL'"
    v-bind:points="command[1]"
    v-bind:style="`fill:none;stroke:${getRandomColor()};stroke-width:4`"
  />



</template>

<script>
export default {
  name: "Shape",
  props: ["command"],
  methods: {
    getRandomColor() {
        var letters = '0123456789ABCDEF';
        var color = '#';
        for (var i = 0; i < 6; i++) {
            color += letters[Math.floor(Math.random() * 16)];
        }
        return color;
    }
  }
};
</script>

<style scoped>
  .shape:hover{
    animation: warp 3s linear 0.1s infinite;
  }

  @keyframes warp {
    0%   {fill: #9400D3}
    14.3%  {fill: #4B0082}
    28.6%  {fill: #0000FF}
    42.9%  {fill: #00FF00}
    57.1% {fill: #FFFF00}
    71.4% {fill: #FF7F00}
    85.7% {fill: #FF0000}
    100% {fill: #9400D3}
  }
</style>
