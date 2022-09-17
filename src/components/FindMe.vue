<template>
  <div>
    <div>
      <div v-if="!toggleStart" style="text-align: center;">Pilih salah satu kotak yang tersedia</div>
      <div v-else style="text-align: center;">Cari Tulisan berwarna merah</div>
    </div>
    <div v-if="toggleFinish" style="text-align: center;">{{ result }}</div>
    <div class="divBox">
      <div @click="clickDiv(boxIndex,index)" v-for="(_,index) in box" class="box" :style="{
        color: boxIndex == index ? 'red' : 'black',
      }">{{ boxText }}</div>
    </div>
    <div class="buttonGroup">
      <span>Waktu : {{ watchTimer }} detik.</span>
      <button @click="move" :disabled="toggleStart">Mulai</button>
      <button @click="reset" :disabled="toggleStart == false">Reset</button>
    </div>
  </div>
</template>

<style scoped>

</style>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  name: "FindMe",
  data: () => ({
    watchTimer: 5,
    box: new Array(4).fill(""),
    boxIndex: 0,
    boxText: 'Aku',
    toggleStart: false,
    toggleFinish: false,
    result: '',
    divClick: false,
  }),
  methods: {
    clickDiv(boxIndex: number, index: number) {
      if (this.toggleStart) {
        if (this.watchTimer == 0) {
          if (!this.divClick) {
            this.divClick = true
            if (boxIndex == index) {
              this.result = 'Menang';
            } else {
              this.result = 'Kalah'
            }
            this.toggleFinish = true
            this.boxText = 'Aku';
          }
        }
      }
    },
    move() {
      let id = setInterval(frame, 1000);
      let self = this
      function frame() {
        let random = Math.floor(Math.random() * self.box.length);
        if (self.watchTimer <= 0) {
          self.watchTimer = 0;
          clearInterval(id)
          self.boxText = ''
        } else {
          console.log(random);
          self.watchTimer--;
          self.boxIndex = random
          self.boxText = 'Aku'
        }
      }
      this.toggleStart = true
    },
    reset() {
      this.watchTimer = 5;
      this.toggleStart = false
      this.toggleFinish = false
      this.divClick = false
    }
  }
})
</script>