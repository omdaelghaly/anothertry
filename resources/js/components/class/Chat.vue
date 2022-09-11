
<template>
  <div>

    <!-- <link rel="stylesheet" href="emojionearea/dist/emojionearea.min.css" /> -->
      <meta charset="UTF-8">

      <!--  bodychat---------------------------------------------- -->
<div class="col-12 border border-dark">
  <div class="row">  

   <!-- ----------------------------------buuton ------------------------------ -->
              <div class="container   " >
                <div style="background:gray">

                 <button type="button" class="btn btn-primary btn-sm">chat</button>
                <button type="button" class="btn btn-primary btn-sm">PM</button>
                <button type="button" class="btn btn-primary btn-sm">users</button>
                </div>
               </div>

      <!-- ---------------------------------------------------------------------- -->
        <div id="chatbody" ref="chatbody" class="chatbody col-12  pl-3 "
          style="height: 430px; overflow-y: scroll; overflow-x:hidden;scroll-behavior: smooth;">
          
        <div id="chatmessage" v-for="(message,index) in messages" :key="index" class="d-flex m-1  " style="overflow-wrap: break-word;">
           <span><h5 style="color:red"> {{message.user.name}}</h5></span>
           <span class=" emojiandtext m-1 px-2" style="background:lightgray;border-radius:0 20px;color:blue;
                ">
            <h5> {{message.msg}}</h5> </span>
        </div>
         
        </div>

        <div class="notify col-12 pl-3">notifyrr
          
        </div>

      <!-- buton send ---------------------------------->
     <div class="col-12  ">
    <div class=" row border border-dark  mx-3 mb-2 p-1  " style="border-radius: 30px" >
      
      <div class="col-10 p-0 mx-auto">
        <input name="" id="textid" class="form-control ml-1 border-0"  style="width: 100%;height: 100%;" />
      </div>

     <button @click="sendmsg"  class="btn btn-primary mx-auto " style="border-radius: 0 30px 30px 30px">send</button>
    </div>
  </div>

      <!-- ------------------------------- -->



      
</div>     
</div>
  </div>
</template>



<style>

</style>

<script type="text/javascript">
    
</script>

<script>
import emojicss from '/node_modules/emojioneArea/dist/emojionearea.min.css'
export default {
  emojicss,
  props:['room'],
  data() {
    return {
             currentroom:this.$route.params.room,
             message:'',
             messages:[],
             user:this.$store.getters.user,
             oldroom:this.$store.getters.oldroom,
     };
  },
  methods:{
      scrolldown(){
         setTimeout(() => {
          var chatbody= document.getElementById("chatbody");
           chatbody.scrollTop=chatbody.scrollHeight
         }, 1000);

      },
      sendmsg(){
        
       var msgarea=$("#textid").emojioneArea();
       var aa =$("#textid")[0].emojioneArea.getText();
         socket.emit('msg',aa,this.currentroom,this.$store.getters.user );
         this.message=''
         msgarea[0].emojioneArea.setText('');    

      }
  },
  created(){
       if(this.oldroom !=''){ socket.emit('leave-room',this.oldroom)};
          
          peer.on('open', function(id) {
 	           console.log('My peer ID is: ' +id);
           socket.emit('join-room',this.currentroom,id);

           });

      socket.on('nmsg',(data)=>{
      this.messages.push(data);
            this.scrolldown();
      })
      
       

    $(document).ready(function () {
      $("#textid").emojioneArea();
    });


  },
  
  mounted() {
     $(document).ready(function () {
    //   $("#textid").emojioneArea();

      //var chatbody= document.getElementById("chatbody");
       
    });

  },
   beforeDestroy() {
            this.$store.commit('setoldroom',this.currentroom);
             // socket.emit('leave-room',this.currentroom)
           //console.log('beforeDestroy');
    },
};
</script>

<style>
</style>