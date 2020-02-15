<template>
    <div class="outer">
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
            <div>Hint: Try some of the following commands!</div>
            <div class="command">
                <ul>
                    <li>
                        p 100,10 40,198 190,78 10,78 160,198
                    </li>
                    <li>
                        p 75,250 80,240 60,200 82,132 43,90 25,50 65,65 117,108 130,103 173,103 187,108 260,70 280,75 275,90 228,138 235,150 265,250
                    </li>
                    <li>
                        p 43,90 25,50 45,57
                    </li>
                </ul>
                
            </div>
        </div>

        <textarea
            name="input"
            id
            cols="30"
            rows="10"
            placeholder="Input your instructions here..."
            @input="sendInstructions"
        ></textarea>
        <div id="error"></div>
    </div>
</template>

<script>
export default {
    name: "InputSection",
    methods: {
        sendInstructions(e) {
            let validCommands = [
                { command: "R", min: 4 , max: 4, csv: false},
                { command: "C", min: 3 , max: 3, csv: false},
                { command: "P", min: 3 , max: false, csv: true},
                { command: "E", min: 4 , max: 4, csv: false},
                { command: "L", min: 5, max: 5, csv: false}
            ];
            let commands = e.target.value.split("\n");
            if (commands.length == 1 && commands[0] == "") {
                showError("");
                this.$emit('add-shapes', [])
                return;
            }

            let checkedCommands = [];
            let invalidCommands = [];

            commands.forEach((command, idx) => {
                let commandResult = validateCommandFormat(command, validCommands);
                if (commandResult) {
                    checkedCommands.push(commandResult);
                } else {
                    invalidCommands.push(idx + 1);
                }
            });

            if (invalidCommands.length > 0) {
                showError(`Error on line/s ${invalidCommands}`);
            } else {
                showError("");
                this.$emit('add-shapes', checkedCommands)
            }

            function showError(err){
                document.querySelector("#error").innerHTML = err;
            }

            function validateCommandFormat(command, validCommands) {
                let cmdArr = command.split(" ");
                cmdArr[0] = cmdArr[0].toUpperCase();
                // let validState = false;
                // check if all parameters are not empty, and if not true, return with false
                // note that this covers cases where a space is at the end
                if (!cmdArr.every(val => val !== "")) {
                    return false;
                }

                let validCommand = false;

                // return true if at least one command is valid, otherwise returns false
                validCommands.some(validCmd => {

                    // check if first argument is a known command and that the number of following parameters is at least min required
                    if (cmdArr[0] === validCmd.command && cmdArr.length - 1 >= validCmd.min){

                        // if max is not required it begins as false, flip it to be true and continue
                        // if max is required it begins as truthy so flip it to only check if the length is less than the max required
                        if (!validCmd.max || cmdArr.length - 1 <= validCmd.max ){

                            // now check if the inputs are valid types
                            let args = (cmdArr.slice(1));
                            if (validCmd.csv) {
                                // split each by comma and check if all are numeric and not empty
                                args = args.map(arg => arg.split(','));
                                if (args.every(splitArg => {
                                    if (splitArg.length !== 2) { return false }
                                    return splitArg.every(el => {
                                        return !isNaN(el) && el !== ""
                                    })
                                })) {
                                    // set validCommand to original input, but join arguments with spaces for easier handling
                                    validCommand = [cmdArr[0], args.join(' ')]
                                    return true;
                                }
                            } else {
                                // if all arguments are numeric, set the validCommand to be the original input and return
                                if (args.every(arg => !isNaN(arg))) {
                                    validCommand = cmdArr;
                                    // note that this is an inner return to get out of the 'some' loop
                                    return true;
                                }
                            }
                        }
                    }
                })

                return validCommand;
            }
        }
    }
};
</script>

<style scoped>
div.outer {
  padding: 30px 0;
}

div.instructions,
div#error {
  text-align: left;
  margin: 0 auto;
  width: 90%;
}

div#error {
  color: #c83939;
  font-style: italic;
  height: 1em;
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

/* when large enough, make display inline */
@media (min-width: 576px) {
    .title{
        width: 90px;
        display: inline-block;
    }
}




textarea {
  background: #f4f4f4;
  width: 90%;
  height: 100px;
  resize: vertical;
  padding: 1em 25px;
  line-height: 2em;
  margin-top: 15px;
}
textarea:focus {
  /* border: none; */
  outline: 1px solid black;
}
</style>
