<template>
 <div class="is-user-avatar-wrapper" >
   <div class="avatar-upload">
        <div class="avatar-edit"
         >
         
            <label
        :style="{background:`${avatar.color}`}"
            
             for="imageUpload"></label>
        </div>
        <div class="avatar-preview"
        :class="{'active':avatar.id ===active}"
        >
            <div id="imagePreview" :style="{backgroundImage: `url(http://i.pravatar.cc/500?img=${avatar.name||7})`}">
            </div>
        </div>
    </div>
    <!-- <div  class="is-user-avatar" >
    <div :style="{background:`${avatar.color}`}" class="color"></div>
    <img :src="newUserAvatar" :alt="avatar.name" />
  </div> -->
    <h6>{{avatar.name&&avatar.name.split(' ')[0]}}</h6>
 </div>

</template>

<script>

export default {
  name: "UserAvatar",
  props: {
    avatar: {
      type: String,
      default: null
    },
    active: {
      type: String,
      default: null
    }
  },
  computed: {
    newUserAvatar() {
         let name = "somename";

      if (this.avatar) {
        name = this.avatar.name;
      }





      return `https://avatars.dicebear.com/v2/human/${name}.svg?options[mood][]=happy`;
    },

  }
};
</script>

<style >
.color{
  width: 15px;
  height:15px;
  border-radius: 50%;
  position: absolute;
  top: 10px;
  left: 0px;
}
.is-user-avatar-wrapper{
    margin-right: 10px;
 
}
.is-user-avatar-wrapper h6{
  text-align: center;
  color: #000;
  margin-top: .5rem;
}
  .is-user-avatar {
     display: inline-block;
    text-align: center;
    height: 70px;
    width: 70px;
    position: relative;
     background: #ffffffcc;
    box-shadow: 1px 1px 5px #15020270;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
    border-radius: 50%;
  }
   .is-user-avatar.active{
     background: #7df38d;

   }
   .is-user-avatar img{
    width: 36px ;
    height: 36px;
    border-radius: 50%;
  }
</style>