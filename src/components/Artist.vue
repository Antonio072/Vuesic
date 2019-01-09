<template lang="pug">
  li.artist
    h2: a(:href="artist.url" target="_blank") {{ artist.name }}
    
    img(:src="artist.image[2]['#text']")  
</template>
    
<script>
export default {
    name: 'artist', 
  props:['artist'] 
}
</script>

<style lang="stylus" scoped>
li.artist
    margin 10px 0px 10px 10px
    padding 10px
    border 3px solid #42b983 
</style>
