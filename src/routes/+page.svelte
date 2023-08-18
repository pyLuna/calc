<script lang="ts">
    let ans = '0';
    let sqrt = '&radic;';
    let oprt = "";
    let chk = false;

    function Squared(num: number): number{
        return Math.sqrt(num);
    }
    function Factorial(num:number): number{
        if(num == 1){
            return num;
        }
        return num * Factorial(num-1);
    }
    function AddZero(inc: number){
        let i = 0;
        while(i < inc){
            ans += '0';
            i++;
        }
    }
    function Append(num:any){
        if(endsWithOperator(ans) && isNaN(num)){ 
            return; 
        }
        if(chk){
            if(!isNaN(num)){
                Clear();                
            }
            chk = false;
        }
        if(num === '!'){
            if(ans.includes('!')){return;}
            oprt = 'fact';
        }
        if(ans === '0'){
            ans = "";
        }
        if(num === 'sq'){
            ans += sqrt;
            oprt = 'sq';
            return;
        }
        ans += num;
    }
    function endsWithOperator(str: string) {
        var lastChar = str.charAt(str.length - 1);
        return lastChar === '+' || lastChar === '-' || lastChar === '/' || lastChar === '*';
    }
    function Equal(){
        if(oprt === ""){
            ans = eval(ans);
            chk = true;
            return;
        }
        if(oprt === 'fact'){
            oprt = "";
            return ans = String(Factorial(Number(ans.slice(0,-1))));
        }
        if(oprt === "sq"){
            oprt = "";
            return ans = String(Squared(Number(ans.replace('&radic;',''))));
        }
    }
    function Clear(){
        ans = '0';
    }
    function Backspace(){
        ans = ans.slice(0,-1);
        if(ans.length === 0){
            ans = '0';
        }
    }
</script>

<table>
    <tr>
        <th colspan="4"><span class="header" id="ans">{@html ans}</span></th>
    </tr>
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