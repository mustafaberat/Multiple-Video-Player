<template>
  <div class="video">
    <Media 
      :kind="'video'"
      :src="'http://media.w3.org/2010/05/sintel/trailer.mp4'"
      :poster="'https://www.freeiconspng.com/uploads/video-icon-0.jpg'"
      :autoplay="true"
      :controls="true"
      :loop="true"
      @pause="handle"
      ref="'fish'"
      style="width: 500px"
      :muted="muted"
    >
    </Media>
    <label class="lbl">default tek link tarafindan gelmistir. Degistirmelidir</label>
  </div>
</template>

<script>
import Media from './videolar'

export default {
  components: {
   Media
  },
  data () {
    return {
      muted: true
    }
  },
  name: 'Video',
  methods: {
    handle() {
      setTimeout( () => {
        this.$refs.fish.play() 
      }, 2000)
    }
  }
}
</script>


<style scoped>
.video{
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
  align-items: center;
}
</style>