<template>
    <div id="option-app">
        <div id="container">
            <h2>Lựa chọn môn học</h2>
            <div>
                <div class="list">
                    <div 
                    :class='{subject: true, selected: sub.select == true}' 
                    v-for="(sub, index) in subjects" 
                    :key="index" 
                    @click="sub.select = !sub.select; solve(subjectsSelected); toRight = true; toLeft= false">
                        {{sub.content}}
                    </div>
                </div>
                <div id="btn">
                    <button 
                    :disabled="(toLeft == true)"  
                    @click="change(subjects, subjectsSelected)">
                    sang trái
                    </button>
                    <button 
                    :disabled="(toRight == true)" 
                    @click="change(subjectsSelected, subjects)">
                    sang phải
                    </button>
                </div>
                <div class="list">
                    <div 
                    :class='{subject: true, selected: sub.select == true}' 
                    v-for="(sub, index) in subjectsSelected" 
                    :key="index" 
                    @click="sub.select = !sub.select; solve(subjects); toLeft = true; toRight = false">
                        {{sub.content}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            select:'',
            check:'',
            toLeft: false,
            toRight: false,
            subjects: [
                {content: "html", select: false},
                {content: "css", select: false},
                {content: "javascript", select: false},
                {content: "vuejs", select: false},
                {content: "reactjs", select: false},
            ],
            subjectsSelected: [
                {content: "PHP", select: false},
                {content: "C++", select: false},
            ]
        }
    },
    methods:{
        solve(dom){
            dom.forEach(a => a.select = false);
        },
        change(before, after){
            var temp1 = before.filter(bef => bef.select);
            var temp2 = before.filter(bef => !bef.select);
            before.splice(0,before.length);
            temp2.forEach(a => before.push(a));
            temp1.forEach(a => after.push(a));
            this.solve(before); 
            this.solve(after);
        }
    }
}
</script>
<style lang="scss" scoped>
    #container{
        width: 600px;
        border: 2px solid #ebebeb;
        margin: 50px auto;
        h2{
            text-align: center;
            background: rgb(76, 202, 76);
            height: 60px;
            line-height: 60px;
            margin-top: 0px;
            margin-bottom: 0px;
            color: rgb(73, 66, 66);
            text-transform: uppercase;
        }
        >div{
            display: flex;
            height: 400px;
            >div{
                flex-grow: 2;
                border: 1px solid #ebebeb;
            }
            >div:nth-child(2){
                flex-grow: 1;
            }
            #btn{
                display: flex;
                flex-direction: column;
                justify-content: center;
            }
            #btn{
                button{
                    width: 70%;
                    margin:10px auto;
                    cursor: pointer;
                    height: 40px;
                    font-weight: bold;
                }
                button:hover{
                    background: #9c9c9c;
                    color: white;
                }
                button:active{
                    background:#4e4e4e;
                }
            }
        }
        
    }
    .list{
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center; 
        text-align: center;
    }
    .subject{
        border:1px solid rgb(185, 184, 184);
        width:80%;
        height: 30px;
        line-height: 30px;
        color:#082e0a;
        border-radius: 10px;
        cursor: pointer;
        background: #ebebeb;
        text-transform: uppercase;
    }
    .selected{
        background:black;
    }
</style>