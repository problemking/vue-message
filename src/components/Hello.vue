<template>
  <div class="hello">
    <h2>{{ msg }}</h2>
    <div class="takeComment">
        <textarea name="textarea" class="takeTextField" id="tijiaoText" v-model="text"></textarea>
        <div class="takeSbmComment">
            <input type="button" class="inputs" value=" " @click="add" />
            <span>(可按 Enter 回复)</span>
        </div>
    </div>
    <div class="commentOn">
        <div class="noContent" v-show="msgData.length==0">暂无留言</div>
        <div class="messList">
        	<div class="reply" v-for="item in msgData" v-cloak>
                <p class="replyContent" style="text-align:left">{{item.content}}</p>
                <p class="operation">
                    <span class="replyTime">发表日期：{{item.time | time}}</span>
                    <span class="handle">
                    	<a href="javascript:;" class="top">{{item.acc}}</a>
                        <a href="javascript:;" class="down_icon">{{item.ref}}</a>
                        <a href="javascript:;" class="cut">删除</a>
                    </span>
                </p>
            </div>
        </div>
        <div class="page">
        	<a href="javascript:;" class="active">1</a>
        	<a href="javascript:;">2</a>
        	<a href="javascript:;">3</a>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: '请在下方发表留言',
      text:'',
      msgData:[]
    }
  },
 
  methods:{
    add() {
        this.$http({
          url:"http://localhost:80/response.php?act=add&content="+this.text,
          header:{
            ContentType:"application/x-www-form-urlencoded"
          }
        }).then(function(res){
           var json=res.data;
           this.msgData.unshift({
                content:this.text,
                time:json.time,
                acc:0,
                ref:0,
                id:json.id
             });
            this.text='';
        })
    },   
    //  add结束
    getPageData:function(n) {
      this.$http({
                  url:"http://localhost:80/response.php?act=get&page="+n,
                  header:{
                      ContentType:"application/x-www-form-urlencoded"
                  }
                }).then(function(res){
                  var el=this
                  var arr=res.data;
                  arr.forEach(function(item){
                  el.msgData.push({
                      content:item.content,
                      time:item.time,
                      acc:item.acc,
                      ref:item.ref,
                      id:item.id
                });
            })
        })
    } 
  },
  // methods结束
   created() {
       this.getPageData(1)
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@charset "utf-8";body,ul,ol,li,dl,dt,dd,p,h1,h2,h3,h4,h5,h6,form,fieldset,table,td,img,div{margin:0;padding:0;border:0}
body{font-size:12px;font-family:"Microsoft YaHei"}
ul,ol{list-style-type:none}
select,input,img,select{vertical-align:middle}
a{text-decoration:underline;color:#313030}
a{blr:expression(this.onFocus=this.blur())}
input,textarea{outline:0;resize:none}
a{outline:0}
.takeComment,.commentOn{margin:0 auto}
.znsArea{width:755px;overflow:hidden;margin:0 auto;font-family:"Microsoft YaHei"}
.commentOn{width:753px;display:block;overflow:hidden;border:#a5bcff solid 1px;background:#f3f8fd;margin-top:25px;font-family:Verdana}
.reply{overflow:hidden;padding:10px 20px;background:#FFF;border-top:#e9e9e9 solid 1px;border-bottom:#e9e9e9 solid 1px}
.userInfo{display:block;overflow:hidden;height:25px;border-bottom:#bababa solid 1px}
.userName{float:left;background:url(img/userBj.png) left center no-repeat;padding-left:15px;color:#000;font-size:14px;font-weight:bold}
.replyTime{float:left;color:#8b8585;line-height:30px;font-size:11px;}
.replyContent{line-height:24px;font-size:14px;color:#2b2b2b;font-family:"Microsoft YaHei"}
.operation{clear:both;width:100%;height:30px;margin-top:8px}
.handle{float:right;padding-top:6px}
.handle a{text-decoration:none;float:left;margin-left:12px;background:url(img/icons.png) 0 0 no-repeat;height:18px;line-height:18px;padding-left:20px}
.handle .top_icon{background-position:0 0}
.handle .down_icon{background-position:0 -17px}
.handle .cut{background-position:0 -33px}
.handle a:active{color:#09F}
.noContent{text-align:center;display:block;background:#FFF;font:14px/2.3 "Microsoft YaHei";border-bottom:#e9e9e9 solid 1px;border-top:#e9e9e9 solid 1px;color:#999}
.takeComment{width:713px;display:block;overflow:hidden;border:#a5bcff solid 1px;background:#f3f8fd;margin-top:25px;font-family:Verdana;padding:15px 20px}
.takeTextField{width:701px;height:70px;border:#b1b1b1 solid 1px;clear:both;display:block;margin:10px 0 10px 0;line-height:20px;padding:5px;box-shadow:inset 0 0 5px #DDD;font-family:"Microsoft YaHei"}
.takeSbmComment{display:block;overflow:hidden}
.takeSbmComment span{float:right;color:#CCC;line-height:37px;padding-right:10px}
.inputs{float:right;width:125px;height:37px;border:none 0;background:tranparent;background:url(img/takeSbmComment.png) left top no-repeat;cursor:pointer;opacity:.8}
.inputs:hover{opacity:1}
.inputs:active{opacity:.9}
.messList{overflow:hidden}
.page{text-align:right;font-size:0;font-family:Verdana;padding:10px 16px}
.page a{display:inline-block;height:20px;padding:0 7px;border:#CCC solid 1px;font:12px/20px Verdana;text-decoration:none;margin-left:5px;background:#FFF}
.page a:hover{background:#09F;color:#FFF;border-color:#09F}
.page .active{background:#CCC}
.page a:active{opacity:.8}

</style>
