<template>
  <div>
    <nav>
      <ul>
        <li v-for="item,i in items" v-on:click="switchItem(i)" :class="{active: i==current}" :style="{backgroundColor: item.props.color}">
        {{ item.props.name }}
        </li>
      </ul>
    </nav>
    <main>
      <h3>{{ currentItem.props.title }}</h3>
      	  <img :src="currentImage" />
	  <p> {{ currentItem.props.player1 }}</p>
    <p> {{ currentItem.props.player2 }}</p>
    <p> {{ currentItem.props.player3 }}</p>
    <p> {{ currentItem.props.player4 }}</p>

	    </main>
    
  </div> 
</template>

<script>
  module.exports = {
    data: function data() {
      return {
        current: 0,
        size: null
      }
    },
    props: ['items'],
    computed: {
      currentItem: function currentItem() {
        return this.items[this.current]
      },
      currentImageSize: function currentImageSize() {
        return 'image'
      },
      currentImage: function currentImage() {
        return 'assets/' + this.currentItem[this.currentImageSize]
      }
    },
    mounted: function mounted() {
      this.resize()
      window.onresize = this.resize
    },
    methods: {
      resize: function resize() {
        this.size = this.$el.getBoundingClientRect()
      },
      switchItem: function switchItem(i) {
        this.current = i
      }
    }
  }
</script>