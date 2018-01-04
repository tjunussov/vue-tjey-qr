<template lang="pug">
svg(style="width:100%; height:100%" :viewBox="'0 0 '+length+' '+length" preserveAspectRatio="none" x="0" y="0")
  rect(v-if="fill" :width="length" :height="length" fill="'#'+fill" cx="0" cy="0")
  defs
    rect#p(width="1" height="1")
  g(fill="#000000")
    template(v-for="(r, y) in dots" Zv-once)
      template(v-for="(c, x) in r")
        use(v-if="c == 1" :x="x" :y="y" xlink:href="#p")
</template>

<script>
import qrEncoder from 'qr-encoder'

export default {
  name: 'QR',
  props:{
    value:{
      required:true,
    },
    fill:{
      default:"#ffffff"
    },
    prefix:{
      required:false
    }
  },
  computed:{
    length(){
      return this.dots.length
    }
  },
  data () {
    return {
      dots:[]
    }
  },
  watch:{
    value(){
      this.encode()
    }
  },
  mounted(){
    // console.log('mouted qr',this.value);
    if(this.value) this.encode()
  },
  methods:{
    encode(){
      // console.log('encode qr',this.value);
      this.dots = qrEncoder.encode((this.prefix?this.prefix:'')+String(this.value),1);
    }
  }
}


</script>

<style lang="stylus">
    
</style>
