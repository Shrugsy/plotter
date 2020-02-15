<template>
    <div class="outer">
        <Instructions />
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
import Instructions from './Instructions'
export default {
    name: "InputSection",
    components: {Instructions},
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

div#error {
    text-align: left;
    margin: 0 auto;
    width: 90%;
    color: #c83939;
    font-style: italic;
    height: 1em;
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
  outline: 1px solid #3C4856;
}
</style>
