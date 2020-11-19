<template>
  <div class="container">
    <h1>
      <!--      This is the text you just typed in -->
      <span class="typed-text">{{ typeValue }}</span>

      <!--      This should be the Cursor blinking-->
      <!--      TODO: getting this cursor to work-->
      <span class="cursor" :class="{ typing: typeStatus }">&nbsp;&nbsp; </span>
    </h1>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component } from "vue-property-decorator";

@Component
export default class TextAnimation extends Vue {
  // data Object --> VueJS --> data:() => return {typedText:''}
  public typeValue = "";
  public typeStatus = false;
  public typeArray = [
    "Write your text right here",
    "And a second text here if you need one.."
  ];
  public typingSpeed = 100;
  public erasingSpeed = 100;
  public newTextDelay = 2000;
  public typeArrayIndex = 0;
  public charIndex = 0;

  // methods
  public typedText() {
    if (this.charIndex < this.typeArray[this.typeArrayIndex].length) {
      if (!this.typeStatus) {
        this.typeStatus = true;
      }
      this.typeValue += this.typeArray[this.typeArrayIndex].charAt(
        this.charIndex
      );
      this.charIndex += 1;
      setTimeout(this.typedText, this.typingSpeed);
    } else {
      this.typeStatus = false;
      setTimeout(this.eraseText, this.newTextDelay);
    }
  }

  public eraseText() {
    if (this.charIndex > 0) {
      if (!this.typeStatus) {
        this.typeStatus = true;
      }
      this.typeValue = this.typeArray[this.typeArrayIndex].substring(
        0,
        this.charIndex - 1
      );
      this.charIndex -= 1;
      setTimeout(this.eraseText, this.erasingSpeed);
    } else {
      this.typeStatus = false;
      this.typeArrayIndex += 1;
      if (this.typeArrayIndex >= this.typeArray.length) {
        this.typeArrayIndex = 0;
      }
      setTimeout(this.typedText, this.newTextDelay + 200);
    }
  }

  // Lifecycle Hooks
  created() {
    setTimeout(this.typedText, this.newTextDelay + 200);
  }
}
</script>

<style scoped lang="scss">
.container {
  width: 80%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
  text-align: center;
}

h1 {
  font-weight: normal;

  span.typed-text {
    color: #2c8dfb;
    padding: 1rem;
  }

  span.cursor {
    display: inline-block;
    margin-left: 3px;
    width: 4px;
    animation: blink 1s infinite;
  }

  span.cursor.typing {
    animation: none;
  }

  @keyframes blink {
    49% {
      background-color: black;
    }
    50% {
      background-color: transparent;
    }
    99% {
      background-color: transparent;
    }
  }
}
</style>
