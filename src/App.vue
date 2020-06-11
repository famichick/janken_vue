<template>
  <div class="wrap">
    <h1>{{txt}}</h1>
    <div class="hands">
      <i :class="awesome"></i>
    </div>
    <div>
      <button
        v-for="shape in shapes"
        :key="shape.key"
        @click="select(shape.key);isActive=!isActive"
        :class="{btn:isActive}"
      >{{shape.label}}</button>
    </div>

    <div class="result">結果：{{resultTxt}}</div>
    <button @click="retry();isActive=!isActive" :class="{btn:!isActive}">もう一度</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      txt: "じゃーんけん…",
      shapes: [
        { label: "ぐー", key: 0 },
        { label: "ちょき", key: 1 },
        { label: "ぱー", key: 2 }
      ],
      handList: ["fas fa-hand-rock", "fas fa-hand-peace", "fas fa-hand-paper"],
      awesome: "",
      player: "",
      npc: "",
      resultTxt: "",
      timer: null,
      btn: "",
      isActive: false
    };
  },
  mounted() {
    this.start();
  },
  methods: {
    start() {
      this.timer = setInterval(() => {
        this.changeHand();
      }, 50);
    },
    changeHand() {
      let num = Math.floor(Math.random() * this.handList.length);
      this.awesome = this.handList[num];
    },
    select(key) {
      this.player = key;
      this.result();
    },
    result() {
      this.txt = "ぽん！";
      this.npc = Math.floor(Math.random() * 3);
      this.awesome = this.handList[this.npc];
      clearInterval(this.timer);
      switch ((this.player - this.npc + 3) % 3) {
        case 0:
          this.resultTxt = "あいこ";
          break;
        case 1:
          this.resultTxt = "負け";
          break;

        case 2:
          this.resultTxt = "勝ち";
      }
      this.isActive = false;

      console.log(this.isActive);
    },
    retry() {
      this.start();
      this.resultTxt = "";
      this.txt = "じゃーんけん…";
    }
  }
};
</script>

<style>
.wrap {
  text-align: center;
}
.btn {
  pointer-events: none;
  opacity: 0.7;
}
.hands {
  font-size: 100px;
}

.fa-hand-rock {
  color: rgb(255, 82, 241);
}
.fa-hand-peace {
  color: rgb(60, 255, 190);
}

.fa-hand-paper {
  color: rgb(66, 66, 206);
}
.result {
  margin: 1em 0;
}
</style>