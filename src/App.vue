<template>
  <div id="app">
    <h1>@Loskir/emoji-picker</h1>
    <p>Emoji picker for vue</p>

    <EmojiPickerButton v-for="i in 5" :id="i" :key="i"/>

    <transition name="fade-300">
      <emoji-picker
        v-show="emojiPicker.show"
        ref="emojiPicker"
        :left="emojiPicker.left"
        :top="emojiPicker.top"
        @emoji="emojiPicker.onEmoji"/>
    </transition>
  </div>
</template>

<script>
  import EmojiPicker from '../../emoji-picker/EmojiPicker.vue'
  import emojiPickerMixin from '../../emoji-picker/mixin'

  import EmojiPickerButton from '@/components/EmojiPickerButton.vue'

  export default {
    name: 'App',
    mixins: [emojiPickerMixin],
    components: {
      EmojiPicker,

      EmojiPickerButton,
    },
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }


  .fade-300-enter-active, .fade-300-leave-active {
    transition: opacity 300ms
  }

  .fade-300-enter, .fade-300-leave-to {
    opacity: 0
  }
</style>
