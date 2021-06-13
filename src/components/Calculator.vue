<template>
    <div class="calculator">
        <div class="display">
            {{current|| '0'}}
        </div>
        <div @click='clear' class='btn'>C</div>
        <div @click='sign' class='btn'>+/-</div>
        <div @click='percent' class='btn'>%</div>
        <div @click="divide" class='btn operator'>/</div>
        <div @click="append('7')" class='btn'>7</div>
        <div @click="append('8')" class='btn'>8</div>
        <div @click="append('9')" class='btn'>9</div>
        <div @click="times" class='btn operator'>*</div>
        <div @click="append('4')" class='btn'>4</div>
        <div @click="append('5')" class='btn'>5</div>
        <div @click="append('6')" class='btn'>6</div>
        <div @click="minus" class='btn operator'>-</div>
        <div @click="append('1')" class='btn'>1</div>
        <div @click="append('2')" class='btn'>2</div>
        <div @click="append('3')" class='btn'>3</div>
        <div @click="plus" class='btn operator'>+</div>
        <div @click="append('0')" class='btn zero'>0</div>
        <div @click="dot" class='btn'>.</div>
        <div @click="equal" class='btn operator'>=</div>
    </div>
</template>

<script>
export default{
    data(){
        return {
            current:'',
            operator:null,
            operatorClicked:false,
            previous:null
        }
    },
    methods:{
        clear(){
            this.current = '';
        },
        sign(){
            this.current =  this.current.charAt(0) === '-'?this.current.slice(1):`-{this.current}`
        },
        percent(){
            this.current = `${parseFloat(this.current)/100}`
        },
        append(number){
            if(this.operatorClicked){
                this.current='';
                this.operatorClicked=false;
            }
            console.log(number)
            this.current =`${this.current}${number}`;

        },
        dot(){
            if(this.current.indexOf('.')===-1){
                this.append('.')
            }
        },
        divide(){
            this.operator = (a,b)=>a/b;
            this.previous = this.current;
            this.operatorClicked=true;
        },
        times(){
            this.operator = (a,b)=>a*b;
            this.previous = this.current;
            this.operatorClicked=true;
        },
        minus(){
            this.operator = (a,b)=>a-b;
            this.previous = this.current;
            this.operatorClicked=true;
        },
        plus(){
            this.operator = (a,b)=>a+b;
            this.previous = this.current;
            this.operatorClicked=true;
        },
        equal(){
            this.current = `${this.operator(parseFloat(this.current),parseFloat(this.previous))}`
            this.previous = null
        }
    }
}
</script>

<style>
.calculator{
    font-size:60px;
    display:grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(70px,auto)
}
.display{
    grid-column : 1/5;
    background-color: #ccc;
}
.zero{
    grid-column : 1/3;
}
.btn{
    background-color:#eee;
    border:0.5px solid #333;
}
.operator{
    background-color:orange;
}
</style>
