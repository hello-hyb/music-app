<template>
  <div class="box">
      <h1 style="color:cyan">音乐盒</h1>
      <input type="text" class="search" v-model="info" @keydown.enter="ok">
        <div class="content">
            <div class="title">
                <span class="t_name">歌名</span>
                <span class="t_singer">歌手</span>
            </div>
            <ul>
                <li v-for="item of songs" :key="item.id" @dblclick="play(item.id, $event)">{{item.name}}<span class="name">{{item.artists[0].name}}</span></li>
            </ul>
        </div>
        <audio src="#" autoplay class="play" controls></audio>
        
  </div>
</template>

<script>
export default {
    name:'Home',
    data(){
        return{
            info:'',
            songs:[],
        }
    },
    methods:{
        ok(){
           this.axios.get('https://autumnfish.cn/search?keywords='+this.info).then(res =>{
               this.songs = res.data.result.songs
           })
        },
        play(id, event){
            document.querySelector(".play").src = 'https://music.163.com/song/media/outer/url?id='+id+'.mp3'
            document.querySelectorAll('li').forEach(item =>{
                item.style.background = 'tomato'
            })
            event.target.style.background = 'cyan'
            
        } 
    }
}
</script>

<style>
::-webkit-scrollbar{
    display: none;
}
.title{
     width: 500px;
     height: 30px;
     box-sizing: border-box;
     padding-left: 30px;
     font-size: 20px;
     font-weight: bold;

}
.t_name{
    float: left;
}
.t_singer{
    float: right;
}
.box{
    margin: 0 auto;
    text-align: center;
}
.search{
    width: 450px;
    height: 40px;
    border: 1px solid teal;
    outline: none;
    font-size: 18px;
    padding-left: 20px;
}
.content{
    width: 550px;
    height: 350px;
    margin: 5px auto 0 auto;
    overflow: auto;
    overflow-x: auto;
    background: rgba(124, 203, 235,.7);
    border-radius: 10px 10px 0 0;
}
.content ul{
    list-style: none;
    float: left;
    padding-left: 25px;
}
.content ul li{
    width: 500px;
    height: 30px;
    background: tomato;
    margin-top: 10px;
    box-sizing: border-box;
    line-height: 30px;
    padding-right: 20px;
    padding-left: 20px;
    border-radius: 10px;
    text-align: left;
}
.content ul li:hover{
    background: cyan;
}
.play{
     width: 550px;
     height: 50px;
     border: 1px solid none;
     background: #f1f3f4;
     border-radius: 0 0 10px 10px;
}
.name{
    float: right;
    
}
.song_name{
    float: left;
}
</style>