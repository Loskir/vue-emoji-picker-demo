<template>
  <button ref="invoker" @click.stop="toggleEmojiPicker">
    Click me
    <template v-if="lastEmoji">
      <img
        src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAAC0lEQVQYV2NgAAIAAAUAAarVyFEAAAAASUVORK5CYII="
        class="emoji"
        :data-name="lastEmoji.charsName"
        :data-emoji="lastEmoji.emoji"
        :alt="lastEmoji.emoji">
    </template>
  </button>
</template>

<script>
  export default {
    name: 'EmojiPickerButton',
    inject: [
      'emojiPicker_show',
      'emojiPicker_hide',
      'emojiPicker_setPosition',
      'emojiPicker_isShown',
      'emojiPicker_getCurrentButton',
      'emojiPicker_setCurrentButton',
      'emojiPicker_getBoundingClientRect',
      'emojiPicker_setOnEmoji',
      'emojiPicker_setHideTimeout',
      'emojiPicker_clearHideTimeout',
    ],
    props: {
      id: Number,
    },
    data: () => ({
      lastEmoji: undefined,
    }),
    methods: {
      toggleEmojiPicker() {
        if (this.emojiPicker_isShown() && this.emojiPicker_getCurrentButton() === this.id) {
          this.emojiPicker_hide()
        } else {
          this.showEmojiPicker()
        }
      },
      showEmojiPicker() {
        this.emojiPicker_show()
        this.emojiPicker_setCurrentButton(this.id)
        this.emojiPicker_setOnEmoji((emoji) => this.lastEmoji = emoji)
        this.emojiPicker_clearHideTimeout()
        this.updateEmojiPickerPosition()
      },
      updateEmojiPickerPosition() {
        const invoker = this.$refs.invoker

        const bcr = invoker.getBoundingClientRect()

        // const bodyBcr = document.body.getBoundingClientRect()

        this.emojiPicker_setPosition(
          bcr.left + bcr.width - 293 /* hardcode warning! ширина самого пикера */,
          bcr.top + bcr.height + 12,
        )
      },
    },
  }
</script>

<style scoped lang="stylus">
  @import "~@loskir/emoji-sprite-stylesheet/emoji.css"
  @import "~@loskir/emoji-sprite-stylesheet/emoji0.css"
</style>