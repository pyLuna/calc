<script lang="ts">
    let prevNum: int;
    let newNum: int;
    let oprt: string;
    let chk: bool;
    
    function Factorial(num:int): int{
        if(num == 1){
            return num;
        }
        return num * Factorial(num-1);
    }

    function AppendNum(test){
        let ans = document.getElementById("ans");
        if(chk == true){
            Clear();
            chk = false;
        }
        if(ans.innerText === '0'){
            ans.innerText = "";
        }
        if(typeof test === 'string' && ans.innerText !== '0'){
            ans.innerText += '00';
        }
        else{
            ans.innerText += test;
        }
        newNum = Number(ans.innerText);
    }   
    function Operator(opr){
        let ans = document.getElementById("ans");
        prevNum = Number(ans.innerText);
        oprt = opr;
        if(opr.length === 3){
            ans.innerText = "0";
        }
        if(opr === "fact" && ans.innerText.charAt(ans.innerText.length-1) !== '!'){
            ans.innerText += "!";
        }
    } 
    function Equal(){
        let ans = document.getElementById("ans");
        switch (oprt) {
            case "add":
                ans.innerText = prevNum + newNum;
                break;
            case "min":
                ans.innerText = prevNum - newNum;
                break;
            case "div":
                ans.innerText = prevNum / newNum;
                break;
            case "mul":
                ans.innerText = prevNum * newNum;
                break;
            case "fact":
                ans.innerText = String(Factorial(Number(ans.innerText.slice(0,-1))));
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
        ans.innerText = "0";
    }
</script>

<table>
    <tr>
        <th colspan="4"><span class="header" id="ans">0</span></th>
    </tr>
    <tr>
        <td on:click={() => Clear()}>C</td>
        <td on:click={() => Operator('sqrt')}>&radic;</td>
        <td on:click={() => Operator('fact')}>!</td>
        <td on:click={() => Operator('div')}>/</td>
    </tr> 
    <tr>
        <td rowspan="" on:click={() => AppendNum(7)}>7</td>
        <td on:click={() => AppendNum(8)}>8</td>
        <td on:click={() => AppendNum(9)}>9</td>
        <td on:click={() => Operator('mul')}>*</td>
    </tr>
    <tr>
        <td on:click={() => AppendNum(4)}>4</td>
        <td on:click={() => AppendNum(5)}>5</td>
        <td on:click={() => AppendNum(6)}>6</td>
        <td on:click={() => Operator('min')}>-</td>
    </tr>   
    <tr>
        <td on:click={() => AppendNum(1)}>1</td>
        <td on:click={() => AppendNum(2)}>2</td>
        <td on:click={() => AppendNum(3)}>3</td>
        <td rowspan="2" on:click={() => Operator('add')}>+</td>
    </tr>
    <tr>
        <td on:click={() => AppendNum(0)}>0</td>
        <td on:click={() => AppendNum('00')}>00</td>
        <td on:click={() => Equal()}>=</td>
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