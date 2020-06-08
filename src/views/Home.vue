<template>
  <ion-page class="ion-page">
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>Home</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content padding>
      <ion-item>
        <ion-label>输入</ion-label>
        <ion-input placeholder="无键盘" :autofocus="true" ref="focusMe" @ionFocus="inputFocus()"></ion-input>
      </ion-item>
      <div>
        <ion-button @click="openAbout()">About</ion-button>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
// @ is an alias to /src
import { Plugins } from '@capacitor/core';

const { Keyboard } = Plugins;

export default {
  name: 'Home',
  mounted () {
    console.log('focus...')
    this.$refs.focusMe.focus()
    Keyboard.addListener('keyboardWillShow', (info) => {
      console.log('keyboard will show with height', info.keyboardHeight);
      Keyboard.hide();
    });

    Keyboard.addListener('keyboardDidShow', (info) => {
      console.log('keyboard did show with height', info.keyboardHeight);
    });

    Keyboard.addListener('keyboardWillHide', () => {
      console.log('keyboard will hide');
    });

    Keyboard.addListener('keyboardDidHide', () => {
      console.log('keyboard did hide');
    });
  },
  methods: {
    inputFocus() {
      console.log('focus....')
    },
    openAbout() {
      this.$router.push("/about");
    }
  }
}
</script>
