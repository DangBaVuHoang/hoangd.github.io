<template>
  <div id="app">
    <div id="remind">
      <div id="add-work" v-if="add==1">
        <div id="background-add" @click="add=0"></div>
        <div>
            <div id="head">
              Thêm kế hoạch: 
              <button @click="add=0">exit</button>
            </div>
          <div>
            <input type="text" v-model="newplan">
            <button @click="addWork()">add</button>
          </div>
        </div>
      </div>
      <h2>todo app</h2>
      <div id="add-work-icon">
        <span id="add" @click="add=1">new plan</span>
      </div>
      <div id="tag">
        <div @click="i=1;" 
        :class="{selected: i==1}">
            Chưa làm({{willDo.length}})

        </div>
        <div @click="i=2;" 
        :class="{selected: i==2}">
            Đã làm({{didWork.length}})

        </div>
        <div @click="i=3;" 
        :class="{selected: i==3}">
            tất cả({{didWork.length + willDo.length}})

        </div>
      </div>
      <div id="container-content">
        <div v-if="i==1">
          <div 
          v-for="(will,indexWill) in willDo" 
          :key="indexWill" 
          :class="{workName: true, xong: will.done}">
            <div>{{1+indexWill}}. {{will.content}}</div>
            <div>
              <button 
              @click="will.done = !will.done" 
              v-if="!will.done">
                  done
              </button>
              <button 
              @click="will.done = !will.done" 
              v-if="will.done" 
              class="undo">
                  undo
              </button>
              <button 
              @click="release(willDo, indexWill)">
                  Xóa
              </button>
            </div>
          </div>
        </div>
        <div v-if="i==2">
          <div 
          v-for="(did,indexDid) in didWork" 
          :key="indexDid" 
          :class="{workName: true, xong: did.done}">
            <div>{{1+indexDid}}. {{did.content}}</div>
            <div>
              <button 
              @click="did.done = !did.done" 
              v-if="!did.done">
                  done

              </button>
              <button 
              @click="did.done = !did.done" 
              v-if="did.done" 
              class="undo">
                  undo

              </button>
              <button 
              @click="release(didWork, indexDid)">
                  Xóa

              </button>
            </div>
          </div>
        </div>
        <div v-if="i==3">
          <div 
          v-for="(will,indexWill) in willDo" 
          :key="`A-${indexWill}`" 
          :class="{workName: true, xong: will.done}">
            <div>{{1+indexWill}}. {{will.content}}</div>
            <div>
              <button 
              @click="will.done = !will.done" 
              v-if="!will.done">
                  done

              </button>
              <button 
              @click="will.done = !will.done" 
              v-if="will.done" 
              class="undo">
                  undo

              </button>
              <button 
              @click="release(willDo, indexWill)">
                  Xóa

              </button>
            </div>
          </div>
          <div 
          v-for="(did,indexDid) in didWork" 
          :key="`B-${indexDid}`" 
          :class="{workName: true, xong: did.done}">
            <div>{{1+willDo.length+indexDid}}. {{did.content}}</div>
            <div>
              <button 
              @click="did.done = !did.done" 
              v-if="!did.done">
                  done

              </button>
              <button 
              @click="did.done = !did.done" 
              v-if="did.done" class="undo">
                  undo

              </button>
              <button 
              @click="release(didWork, indexDid)">
                  Xóa

              </button>
            </div>
          </div>
        </div>
      </div>
      <div id="save">
        <button @click="reLoad(willDo, didWork);">save</button>
      </div>
    </div>
    <div id="choose">
    </div>
  </div>
</template>

<script>

export default {
  data(){
    return{
      newplan: '',
      i: 1,
      add: 0,
      willDo: [
        {content:'Nấu ăn' , done: false},
        {content:'Lau nhà' , done: false},
        {content:'rửa bát' , done: false},
      ],  
      didWork: [
        {content:"Thức dậy", done: true},
        {content:"Đánh răng", done: true},
      ]
    }
  },
  methods: {
    addWork(){
      if(this.newplan != ''){
        this.willDo.push({content: this.newplan, done: false});
        this.newplan = '';
        this.add=0;
      }
    },
    release: function(work,index){
      work.splice(index,1);
    },
    reLoad: function(){
      var temp1 = this.willDo.filter(work => work.done);
      var temp2 = this.didWork.filter(work => !work.done);
      this.willDo    = this.willDo.filter(work => !work.done);
      this.didWork     = this.didWork.filter(work => work.done);
      temp2.forEach(element => {
        this.willDo.push(element);
      });
      temp1.forEach(element => {
        this.didWork.push(element);
      });
    }
  }
}
</script>

<style lang="scss" scoped>
  *{
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
    border-radius: 5px;
  }
  h2{
    padding-top: 10px;
    text-transform: uppercase; 
    color: rgb(235, 235, 235);
    text-align: center;
    background: rgb(3, 187, 233);
    height: 50px;
  }
  #add-work-icon{
    height: 30px;
    position: relative;
    margin-top: 10px;
    margin-bottom: 10px;
  }
  #add{
    text-transform: uppercase;
    position: absolute;
    display: inline-block;
    width: 145px;
    text-align: center;
    padding-left: 5px;
    height: 30px;
    line-height: 28px;
    cursor: pointer;
    top: 3px;
    right: 31px;
    border: 2px solid white;
    color: rgb(255, 255, 255);
    font-weight: bold;
    background: #240cfa;
    border-radius: 30px;
  }
  #remind {
    max-width: 500px;
    background: #d6d6d6;
    margin: 10px auto;
    padding-bottom: 40px;
    position: relative;
  }
  #add-work{
    position: absolute;
    width: 100%;
    height: 100%;
    #background-add{
      position: absolute;
      width: 100%;
      height: 100%;
      top: 0px;
      left: 0px;
      z-index: 1;
      background: rgba(161, 160, 160, 0.267); 
      cursor: pointer;
    }
    > div{
      position: absolute;
      width: 70%;
      height: 32%;
      top: 25%;
      left: 15%;
      z-index: 2;
      background: white;
      div:first-child{
        color: green;
        font-size: 20px;
        border-bottom: 2px solid #ebebeb;
        height: 50px;
        line-height: 50px;
        padding-left: 10px;
      }
      button{
        height: 30px;
        width: 200px;
        position: absolute;
        bottom: 10px;
        right: 10px;
        cursor: pointer;
      }
      button:hover{
        background: rgb(100, 100, 100);
        color:white;
      }
      button:active{
        background: rgb(43, 43, 43);
      }
    }
    input{
      width: 96%;
      height: 30px;
      font-size: 15px;
      padding: 10px;
      margin-left:2%;
      margin-top: 10px;
      border: 2px solid #c9c7c7;
    }
    #head{
        position: relative;
        button{
            position: absolute;
            top: 8px;
            right: 10px;
            width: 80px;
            font-size:15px;
            border-radius: 30px;
        }
    }
  }
  #tag{
    padding: 5px;
    display: flex;
    justify-content: center;
  }
  #tag {
    *{
      width: 30%;
      text-align: center;
      background: rgb(255, 255, 255);
      border: 2px solid #d6d6d6;
      line-height: 50px;
      cursor: pointer;
    }
    *:hover{
      background: #e9e8e8a6;
    }
  }
  #container-content{
    width: 90%;
    height: 300px;
    margin: 10px auto;
    background: rgb(255, 255, 255);
    overflow: scroll;
  }
  .xong{
    text-decoration: line-through;
    color: green;
  }
  .selected{
    background: #b1b1b1 !important;
  }
  .workName{
    // transform: translateX(100vw);
    margin: 5px;
    height: 30px;
    line-height: 27px;
    border: 1px solid #ebebeb;
    display: flex;
    justify-content: space-between;
    padding-left: 10px;
    padding-right: 10px;
    div:first-child{
      width: 65%;
      overflow: hidden;
    }
    div:nth-child(2){
        width: 122px;
    }
    button{
      margin-left: 10px;
      padding: 3px 10px;
      cursor: pointer;
    }
  }
  .undo{
    color: white;
    background: rgb(85, 85, 85);
  }
  #save{
    position: absolute;
    right: 30px;
    bottom: 10px;
    width: 100px;
    height: 30px;
    button{
      width: 100%;
      height: 100%;
      cursor: pointer;
      background: rgb(12, 250, 12);
      border:1px solid rgb(235, 235, 235);
      color: rgb(0, 0, 0);
    }
    button:hover{
      background: rgb(103, 240, 98);
    }
    button:active{
      background: rgb(170, 167, 167);
      border:1px solid rgb(235, 235, 235);
    }
  }
</style>
