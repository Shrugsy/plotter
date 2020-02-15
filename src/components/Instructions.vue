<template>
    <div class="instructions">
        <p>Plot some objects!</p>
        <p>Available commands:</p>
        <ul>
            <li>
                <span class="title">Rectangle:</span>
                <span class="command"
                    >R &lt;X Coordinate&gt; &lt;Y Coordinate&gt; &lt;Width&gt;
                    &lt;Height&gt;</span
                >
            </li>
            <li>
                <span class="title">Circle:</span>
                <span class="command"
                    >C &lt;CX Coordinate&gt; &lt;CY Coordinate&gt; &lt;Radius&gt;
                </span>
            </li>
            <li>
                <span class="title">Polygon:</span>
                <span class="command"
                    >P &lt;X1,Y1&gt; &lt;X2,Y2&gt; &lt;X3,Y3&gt; .....
                    &lt;Xn,Yn&gt;</span
                >
            </li>
            <li>
                <span class="title">Ellipse:</span>
                <span class="command"
                    >E &lt;CX Coordinate&gt; &lt;CY Coordinate&gt; &lt;X Radius&gt; &lt;Y Radius&gt;</span
                >
            </li>
            <li>
                <span class="title">Line:</span>
                <span class="command"
                    >L &lt;X1 Coordinate&gt; &lt;Y1 Coordinate&gt; &lt;X2 Coordinate&gt; &lt;Y2 Coordinate&gt; &lt;Stroke Width&gt;</span
                >
            </li>
        </ul>
        <div>Try some of the following examples!</div>
        <div class="command command-examples">
            <ul>
                <ExampleCommand v-for="(example, idx) in examples" v-bind:example="example" v-bind:key="idx" />                    
            </ul>
            
        </div>
    </div>
</template>

<script>
import ExampleCommand from './ExampleCommand';
export default {
    name: "Instructions",
    components: {
        ExampleCommand
    },
    data() {
        return {
            examples: [{
                title: 'Command 1',
                commands: ['p 81,186 125,50 169,186 54,102 196,102']
            },
            {
                title: 'Command 2',
                commands: [
                    'p 195,54 163,33 123,25 87,33 53,56 33,87 25,127 33,163 55,197 87,217 127,225 163,218 197,195 125,125',
                    'c 145 64 18'
                ]
            },
            {
                title: 'Command 3',
                commands: [
                    'p 75,250 80,240 60,200 82,132 43,90 25,50 65,65 117,108 130,103 173,103 187,108 260,70 280,75 275,90 228,138 235,150 265,250',
                    'p 43,90 25,50 45,57',
                    'e 108 156 10 13',
                    'e 188 156 10 13',
                    'c 106 152 5',
                    'c 186 152 5',
                    'e 141 175 7 5',
                    'p 131,200 135,197 142,194 153,192 158,195 162,198 164,210 162,217 154,219 144,219 136,215 131,209',
                    'e 81 190 13 10',
                    'e 212 190 13 10'
                ]
            }
            ]
        }
    }
}
</script>

<style scoped>
div.instructions {
  text-align: left;
  margin: 0 auto;
  width: 90%;
}

li {
  list-style: none;
  padding-left: 1em;
  line-height: 2em;
}

/* make 100% width for small width to not be too crammed */
.title{
    display: block;
    width: 100%;
}

.command {
    font-style: italic;
    font-size: 0.8em;
}

.command-examples li {
    padding-left: 0;
}

/* when large enough, make display inline */
@media (min-width: 576px) {
    .title{
        width: 90px;
        display: inline-block;
    }
}

</style>