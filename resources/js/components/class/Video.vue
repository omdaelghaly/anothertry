

<template>
    <div>


  <div class="col-12 border border-dark" >  
    <div class="row">
   
        <div class="col-12  p-0     ">
            
            
              <video id="videoid" src="a.mp4"   controls muted  style="width:100%;height:450px;object-fit:fill;"></video>
              
  
              <div class="caption ml-3" style="height:80px">
                <button @click="stream" type="button" class="btn btn-primary btn-sm">Stream</button>
                <button type="button" class="btn btn-primary btn-sm">Small button</button>
     
          </div>

        </div>
        
        
    </div>
  </div>   

    </div>
</template>



<script>
import Chat from './Chat.vue'
export default {
  components: { Chat },
       data(){
         return{
             currentroom:this.$route.params.room,
             user:this.$store.getters.user,
         }
       },
       methods:{
             stream(){
 
  
  
  




//    var vid = document.getElementById('m');

//   var call = peer.call(peerid, stream);
//   call.on('stream', function(remoteStream) {
//     // Show stream in some video/canvas element.
//   });
// }, function(err) {
//   console.log('Failed to get local stream' ,err);


//});

                

             },
             addvideostream(video,stream){
                  video.srcObject = stream;
                  video.load();
                  video.play();
             },
             connectvideostream(pid,stream){
               
               call.on('close',()=>{
                 vid.remove()
               })
             },
                  

       },
       created(){
              
        socket.on('user_connected',(peerid)=>{

      //    var getUserMedia = navigator.getUserMedia ||
      //    navigator.webkitGetUserMedia || navigator.mozGetUserMedia;
      //  getUserMedia({video: true, audio: true}, function(stream) {


      //  });

               navigator.mediaDevices.getUserMedia({
                 video:true,
                 audio:true,
               }).then((stream)=>{
                let call= peer.call(peerid,stream)
                   call.on('stream', function(remotestream){
var videoo= document.getElementById('l');
                   videoo.srcObject = stream;
                  videoo.load();
                  videoo.play();    
                    }) 
               }).catch((error)=>{console.log(error)})

peer.on('call', function(call) {
	// Answer the call, providing our mediaStream
    navigator.mediaDevices.getUserMedia({
                 video:true,
                 audio:true,
    }).then((stream)=>{
	   call.answer(stream);
     call.on('stream', function(remotestream){
var video = document.getElementById('n');
                   video.srcObject =remotestream;
                  video.load();
                  video.play();    
                  
     })

    })
  });

                    });
       }

}
</script>

<style>

</style>