<script lang="ts">
    let prevNum: number;
    let newNum: number;
    let oprt: string;
    let chk: boolean;
    let ans = "0";

    function Factorial(num:number): number{
        if(num == 1){
            return num;
        }
        return num * Factorial(num-1);
    }

    function Squared(num: number): number{
        return Math.sqrt(num);
    }

    function AppendNum(test: any){
        if(chk == true){
            Clear();
            chk = false;
        }
        if(ans === '0'){
            ans = "";
        }
        if(typeof test === 'string' && ans !== '0'){
            ans += '00';
        }
        else{
            ans += test;
        }
        newNum = Number(ans);
    }   
    function Operator(opr: string){
        prevNum = Number(ans);
        oprt = opr;
        // if(opr.length === 3){
        //     ans = "0";
        // }
        if(opr === "fact" && ans.charAt(ans.length-1) !== '!'){
            ans += "!";
        }
        if(opr === "sqrt"){
            prevNum = Number(ans);
            // ans += '&radic';
        }
    }
    function Equal(newNum: any){
        if(Number(ans) === 0){
            ans = "";
        }
        // if(ans.length != 4){
            ans += newNum;
        // }
        switch (oprt) {
            case "add":
                ans = String(prevNum + newNum);
                break;
            case "min":
                ans = String(prevNum - newNum);
                break;
            case "div":
                ans = String(prevNum / newNum);
                break;
            case "mul":
                ans = String(prevNum * newNum);
                break;
            case "fact":
                ans = String(Factorial(Number(ans.slice(0,-1))));
                break;
            case "sqrt":
                ans = String(Squared(newNum));
                break;
            default:
                break;
        }
        chk = true;
    }
    function Clear(){
        prevNum = 0;
        newNum = 0;
        oprt = '';
        ans = "0";
    }
</script>

<table>
    <tr>
        <th colspan="4"><span class="header" id="ans">{@html ans}</span></th>
    </tr>
    <tr>
        <td on:click={() => Clear()}>C</td>
        <td on:click={() => Operator('sqrt')}>&radic;</td>
        <td on:click={() => Operator('fact')}>!</td>
        <td on:click={() => Operator('div')}>/</td>
    </tr> 
    <tr>
        <td on:click={() => Equal(7)}>7</td>
        <td on:click={() => Equal(8)}>8</td>
        <td on:click={() => Equal(9)}>9</td>
        <td on:click={() => Operator('mul')}>*</td>
    </tr>
    <tr>
        <td on:click={() => Equal(4)}>4</td>
        <td on:click={() => Equal(5)}>5</td>
        <td on:click={() => Equal(6)}>6</td>
        <td on:click={() => Operator('min')}>-</td>
    </tr>   
    <tr>
        <td on:click={() => Equal(1)}>1</td>
        <td on:click={() => Equal(2)}>2</td>
        <td on:click={() => Equal(3)}>3</td>
        <td rowspan="2" on:click={() => Operator('add')}>+</td>
    </tr>
    <tr>
        <td on:click={() => Equal(0)}>0</td>
        <td on:click={() => Equal('00')}>00</td>
        <td on:click={() => Equal(ans)}>=</td>
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
        top:20%;
        left: 30%;
    }
    table, th, td {
      border: 1px solid black;
      border-collapse: collapse;
    }
    tr td{
        text-align: center;
    }
    tr td:hover{
        background-color: rgba(31, 31, 32, 0.425);
        cursor: pointer;
    }
    .header{
        float: right;
        margin-right: 30px;
    }
    </style>