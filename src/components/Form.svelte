<script>

    let uppercase = true;
    let lowwercase = true;
    let specialSymbols = true;
    let numbers = true;
    let rangeNum = (localStorage.getItem("range") == null)? 30 : localStorage.getItem("range");
    let randomPasswordOut = '';
    
    

    function generateRandom(numOfChars, hasUpper, hasLower, hasSym, hasNum){

        if(!hasUpper && !hasLower && !hasSym && !hasNum) return "";

        const nums = "1234567890";
        const lowerChars = "abcdefghijklmnopqrstuvwxyz";
        const upperChars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        const symbosl = "!@#$%^&*";

        let arr = [];
        let pass = "";

        if (hasUpper) arr = [upperChars, ...arr]
        if (hasLower) arr = [lowerChars, ...arr]
        if (hasSym)   arr = [symbosl, ...arr]
        if (hasNum)   arr = [nums, ...arr]

        
        for(let i = 0; i < numOfChars; i++){
            const smallRandom = Math.floor(Math.random() * arr.length);
            const bigRandom = Math.floor(Math.random() * arr[smallRandom].length)
            pass += arr[smallRandom][bigRandom]
        }
        
        return pass;
    }

</script>

<div class="formComponent">
    <h3 class="title">Generate password</h3>
    <input type="text" placeholder="Random password" class="input" readonly value={randomPasswordOut}>
        <div class="checkbox">
        <!-- svelte-ignore a11y-label-has-associated-control -->
        <label>Length: {rangeNum} characters!</label>
        <input type="range" on:change={() =>{
            localStorage.setItem("range", rangeNum )
        }} bind:value={rangeNum} min="10" max='128' class="range">
        <input type="checkbox" bind:checked={uppercase}>Uppercase<br>
        <input type="checkbox" bind:checked={lowwercase}>Lowercase<br>
        <input type="checkbox" bind:checked={specialSymbols}>Special symbols<br>
        <input type="checkbox" bind:checked={numbers}>Numbers<br>
    </div>
        <button on:click={ () => {
            randomPasswordOut = generateRandom(rangeNum,uppercase,lowwercase,specialSymbols,numbers)
            } }>Generate</button>
</div>


<style>

    .title{ 
        color: rgba(70,70,70,0.8);
    }

    .input{
        background-color: burlywood;
        width: 70%;
        min-width: 100px;   
    }

    .checkbox{
        padding-top: 0px;
        padding-bottom: 10px;
        width: 200px;
        text-align: left;
        margin-left: 15%; 
    }


    .formComponent{
        background: rgba(0,0,0, 0.3);
        text-align: center;
        border-radius: 20px;
        padding-top: 5px;
        padding-bottom: 30px;
        margin: 5%;
        margin-left: 10%;
        margin-right: 10%;
    }
    button{

        background-color: rgb(37, 22, 4);
        color: white;
        width: 30%;
        min-width: 100px;
        border-radius: 10px;
        
    }

    button:hover{
        background-color: white;
        color: black;
        cursor: pointer;
        transition: 0.3s ease;
    }

    .range{
        width: 100%
    }
</style>