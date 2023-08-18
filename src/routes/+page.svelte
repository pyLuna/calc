<script lang="ts">
    // local variables
    // the answer that will be displayed after calculation
    let ans = '0';
    // square root sign for display
    let sqrt = '&radic;';
    // operator variable made specifically for factorial and square root
    let oprt = "";
    //checker if the math sequence is ended based on user
    let chk = false;

    /*  Squared() function with a parameter named 'num'
     *  This function processed the received number and 
     *  it will find the square root using the Math.sqrt() API
     */
    function Squared(num: number): number{
        return Math.sqrt(num);
    }
    /*  The Factorial() with a parameter named 'num' is a 
     *  simple recursion that will return the factorial of given number
     *  
     *  Example:
     *  if the num is not equal to 1 it will call itself with a
     *  mathematical expression 'num * (num-1)'
     * 
     *  num = 5;
     *  return 5 * Factorial(5-1)
     *  return 4 * Factorial(4-1)
     *  ...
     *  return 2 * Factorial(2-1)
     *  then the Factorial() will return the product when num is equal to 1
    */
    function Factorial(num:number): number{
        if(num == 1){
            return num;
        }
        return num * Factorial(num-1);
    }
    /*
    *   nothing special, just adding a zero to the ans variable
    */
    function AddZero(inc: number){
        let i = 0;
        while(i < inc){
            ans += '0';
            i++;
        }
    }
    /*
    *   check if the received string has operator on the end
    *   This will prevent to add multiple operation in one sequence
    *   using the charAt() API, it will get the last character from string
    *   and the function will return a boolean when the lastChar has [+,-,/,*]
    */ 
    function endsWithOperator(str: string) {
        var lastChar = str.charAt(str.length - 1);
        return lastChar === '+' || lastChar === '-' || lastChar === '/' || lastChar === '*';
    }
    /*
    *   adds a number or operator
    */
    function Append(num:any){
        /*
        *   check the num variable if it has an operator on last index of string
        *   and isNaN() will check if its a number or not
        *   if the condition is true the Append() will disregard the recent input
        *   in this case will be the operator [+,-,/,*]
        */ 

        if(endsWithOperator(String(ans)) && isNaN(num)){ 
            return; 
        }
        /*  the chk variable with "false" boolean value as default 
        *   will be triggered when equal button is clicked
        */
        if(chk){
            // check if the new entered value is a number so the sequence will be reset
            if(!isNaN(num)){
                Clear();                
            }
            chk = false;
        }
        //  check if the value is a exclamation point (factorial symbol)
        if(num === '!'){
            // check if the sequence are already have a factorial symbol
            // and disregard if true
            if(ans.includes('!')){return;}
            //set the operator to 'fact' short as factorial
            oprt = 'fact';
        }
        // clear the ans if the starting value is zero
        if(ans === '0'){
            ans = "";
        }
        // check if the num value is 'sq' so it can proceed to Squared()
        // when equal button is clicked
        if(num === 'sq'){
            ans += sqrt;
            oprt = 'sq';
            return;
        }
        ans += num;
    }
    // this function process the sequence from ans variable
    function Equal(){
        // this will process the sequence
        if(oprt === ""){
            ans = eval(ans);
            chk = true;
            return;
        }
        // filter for factorial and will run when the oprt is set to 'fact'
        if(oprt === 'fact'){
            //change the value of oprt to no value
            oprt = "";
            // ends the function with ans = returned value from Factorial()
            // String() converts the value to string
            // Number() converts the value to number or int
            // replace(itemtoreplace, changeintothisvalue) will replace the '!' into whitespace or null
            return ans = String(Factorial(Number(ans.replace('!',''))));
        }
        // filter for square root and will run when the oprt is set to 'sq'
        if(oprt === "sq"){
            //change the value of oprt to no value
            oprt = "";
            // ends the function with ans = returned value from Squared()
            // '&radic;' is an HTML entity symbol that represents square root
            return ans = String(Squared(Number(ans.replace('&radic;',''))));
        }
    }
    //clear the ans
    function Clear(){
        ans = '0';
    }
    //removes the last character from the ans
    function Backspace(){
        ans = String(ans).slice(0,-1);
        if(ans.length === 0){
            ans = '0';
        }
    }
</script>

<table>
    <tr>
        <!-- will serve as an answer 
             the {@html ans} is where the ans variable will be displayed
        -->
        <th colspan="4"><span class="header" id="ans">{@html ans}</span></th>
    </tr>
    <!-- 
        on:click={} is an event that will be triggered
        when the user clicked the td or the table cell
    -->
    <tr>
        <td on:click={() => Clear()}>C</td>
        <td on:click={() => Append('sq')}>&radic;</td>
        <td on:click={() => Append('!')}>!</td>
        <td on:click={() => Backspace()}>&#8592;</td>
    </tr>
    <tr>
        <td on:click={() => Append(7)}>7</td>
        <td on:click={() => Append(8)}>8</td>
        <td on:click={() => Append(9)}>9</td>
        <td on:click={() => Append('/')}>/</td>
    </tr>
    <tr>
        <td on:click={() => Append(4)}>4</td>
        <td on:click={() => Append(5)}>5</td>
        <td on:click={() => Append(6)}>6</td>
        <td on:click={() => Append('*')}>*</td>
    </tr>   
    <tr>
        <td on:click={() => Append(1)}>1</td>
        <td on:click={() => Append(2)}>2</td>
        <td on:click={() => Append(3)}>3</td>
        <td on:click={() => Append('-')}>-</td>
    </tr>
    <tr>
        <td on:click={() => AddZero(1)}>0</td>
        <td on:click={() => AddZero(2)}>00</td>
        <td on:click={() => Equal()}>=</td>
        <td on:click={() => Append('+')}>+</td>
    </tr>
</table>

<style>
    @font-face{
        font-family: Digital;
        font-style: normal;
        font-weight: 550;
        src: url('/fonts/Digital7-rg1mL.ttf');
    }
    table{
        font-family: Digital;
        width: 600px;
        height: 500px;
        font-size: 40px;
        table-layout: fixed;
        position: absolute;
        top:10%;
        left: 30%;
        border-radius: 30px;
    }
    table, th, td {
      border: 1px solid black;
      border-radius: 10px;
      padding: 25px;
    }
    tr td{
        text-align: center;
        transition: background-color 0.3s ease;
    }
    tr td:hover{
        background-color: rgba(31, 31, 32, 0.425);
        cursor: pointer;
    }
    .header{
        float: right;
        margin-right: 30px;
    }
    table tr th{
        background-color: rgba(96, 97, 99, 0.808);
        border-spacing: 5px;
    }
    </style>