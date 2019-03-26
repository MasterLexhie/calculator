<template>
    <div class="calculator">
        <table cellspacing="10">
            <tr>
                <td colspan="4">
                    <input type="text" v-model="result" disabled>
                </td>
            </tr>
            <tr>
               <td class="button dark" @click="clear">C</td>
               <td class="button dark" @click="invertedNumber">+/-</td>
               <td class="button dark" @click="percentage">%</td>
               <td class="button orange" @click="setOperator('/')">/</td>
            </tr>
            <tr>
               <td class="button grey" @click="numbers(7)">7</td>
               <td class="button grey" @click="numbers(8)">8</td>
               <td class="button grey" @click="numbers(9)">9</td>
               <td class="button orange" @click="setOperator('*')">*</td>
            </tr>
            <tr>
               <td class="button grey" @click="numbers(4)">4</td>
               <td class="button grey" @click="numbers(5)">5</td>
               <td class="button grey" @click="numbers(6)">6</td>
               <td class="button orange" @click="setOperator('-')">-</td>
            </tr>
            <tr>
               <td class="button grey" @click="numbers(1)">1</td>
               <td class="button grey" @click="numbers(2)">2</td>
               <td class="button grey" @click="numbers(3)">3</td>
               <td class="button orange" @click="setOperator('+')">+</td>
            </tr>
            <tr>
               <td colspan="2" class="button button-col2 grey" @click="numbers(0)">0</td>
               <td class="button grey" @click="decimalPoint">.</td>
               <td class="button orange" @click="equal">=</td>
            </tr>
        </table>


    </div>
</template>

<script>
export default {
    data() {
        return {
            result: 0, //number value 
            tmp_value: 0, //temporary value used in calculating
            reset: false,
            operator: undefined // operators used in calculation
        }
    },
    methods:{
        clear(){
            this.result = 0;
            this.tmp_value = 0;
            this.operator = undefined;
        },
        invertedNumber(){
            this.result *= -1;
        },
        percentage(){
            this.result /= 100;
        },
        numbers(num){
            if(this.result === 0 || this.reset === true){
                this.result = '';
                this.reset = false;
            }
            this.result += num.toString();
        },
        decimalPoint(){
            if(!this.result.includes('.'))
            this.result += '.';
        },
        calculate(){
            let value = 0;
            let firstNum = parseFloat(this.tmp_value);
            let secondNum = parseFloat(this.result);

            switch (this.operator) {
                case '+':
                    value = firstNum + secondNum
                break;
                case '-':
                    value = firstNum - secondNum
                break;
                case '*':
                    value = firstNum * secondNum
                break;
                case '/':
                    value = firstNum / secondNum
                break;
            }
            this.result = value;
        },
        setOperator(operator){
            if (this.tmp_value != 0) {
                this.calculate();    
            }
            this.tmp_value = this.result;
            this.operator = operator;
            this.reset = true;
            
        },
        equal(){
            this.calculate();
            this.tmp_value = 0;
            this.operator = undefined

        }

    }
}
</script>
<style scoped>
    .calculator{
        border: 1px solid #fff;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        font-size: 3rem;
    }

    table{
        color: #fff;
        width: 370px;
    }
    
    input{
        display: block;
        /* border: 1px solid #fff; */
        width: calc(100% -  40px);
        height: 75px;
        border: none;
        padding: 5px 20px 0;
        background-color: #222;
        color: #fff;
        font-size: 5rem;
        text-align: right;
    }
    .button{
        margin: 10px;
        border-radius: 40px;
        width: 80px;
        height: 80px;
        text-align: center;
        font-weight: bold;
        cursor: pointer;
    }
    .button-col2{
        border-radius: 40px;
        border: 1px solid #fff;
        width: 160px;
        height: 80px;
        text-align: center;
        font-weight: bold;
        cursor: pointer;
    }
    .grey{
        background-color: #ccc;
        color: #333;

        
    }
    .grey:hover{
        background-color: #ddd;
    }


    .dark{
        background-color: #444;
        color: #fff;
    }

    .dark:hover{
        background-color: #555;
    }

    .orange{
        background-color: #e08d1f;
        color: #fff
    }

    .orange:hover{
        background-color: #fda22b;
    }

   
</style>


