<template>
  <div class="home">
    <p id="msg">发音 平假 片假</p>
    <p id="show"></p>
    <div class="btnContainer">
      <el-button :click="switchDirect(0)" class="btn">顺序</el-button>
      <el-button :click="switchDirect(1)" class="btn">随机</el-button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import data from '../assets/data.js'
export default {
  name: "home",
  components: {},
  data() {
    return {
      NewFlag: true, // 下一个是新的单词还是原来的
      currIndex: 0,
      mode: 1,
      direct: 2,
      wordList: [
        { spell: "a", pingjia: "あ", pianjia: "ア" },
        { spell: "i", pingjia: "い", pianjia: "イ" },
        { spell: "u", pingjia: "う", pianjia: "ウ" },
        { spell: "e", pingjia: "え", pianjia: "エ" },
        { spell: "o", pingjia: "お", pianjia: "オ" },
        { spell: "ka", pingjia: "か", pianjia: "カ" },
        { spell: "ki", pingjia: "き", pianjia: "キ" },
        { spell: "ku", pingjia: "く", pianjia: "ク" },
        { spell: "ke", pingjia: "け", pianjia: "ケ" },
        { spell: "ko", pingjia: "こ", pianjia: "コ" },
        { spell: "sa", pingjia: "さ", pianjia: "サ" },
        { spell: "shi", pingjia: "し", pianjia: "シ" },
        { spell: "su", pingjia: "す", pianjia: "ス" },
        { spell: "se", pingjia: "せ", pianjia: "セ" },
        { spell: "so", pingjia: "そ", pianjia: "ソ" },
        { spell: "ta", pingjia: "た", pianjia: "タ" },
        { spell: "chi", pingjia: "ち", pianjia: "チ" },
        { spell: "tsu", pingjia: "つ", pianjia: "ツ" },
        { spell: "te", pingjia: "て", pianjia: "テ" },
        { spell: "to", pingjia: "と", pianjia: "ト" },
        { spell: "na", pingjia: "な", pianjia: "ナ" },
        { spell: "ni", pingjia: "に", pianjia: "ニ" },
        { spell: "nu", pingjia: "ぬ", pianjia: "ヌ" },
        { spell: "ne", pingjia: "ね", pianjia: "ネ" },
        { spell: "no", pingjia: "の", pianjia: "ノ" },
        { spell: "ha", pingjia: "は", pianjia: "ハ" },
        { spell: "hi", pingjia: "ひ", pianjia: "ヒ" },
        { spell: "fu", pingjia: "ふ", pianjia: "フ" },
        { spell: "he", pingjia: "へ", pianjia: "ヘ" },
        { spell: "ho", pingjia: "ほ", pianjia: "ホ" },
        { spell: "ma", pingjia: "ま", pianjia: "マ" },
        { spell: "mi", pingjia: "み", pianjia: "ミ" },
        { spell: "mu", pingjia: "む", pianjia: "ム" },
        { spell: "me", pingjia: "め", pianjia: "メ" },
        { spell: "mo", pingjia: "も", pianjia: "モ" },
        { spell: "ya", pingjia: "や", pianjia: "ヤ" },
        { spell: "yu", pingjia: "ゆ", pianjia: "ユ" },
        { spell: "yo", pingjia: "よ", pianjia: "ヨ" },
        { spell: "ra", pingjia: "ら", pianjia: "ラ" },
        { spell: "ri", pingjia: "り", pianjia: "リ" },
        { spell: "ru", pingjia: "る", pianjia: "ル" },
        { spell: "re", pingjia: "れ", pianjia: "レ" },
        { spell: "ro", pingjia: "ろ", pianjia: "ロ" },
        { spell: "wa", pingjia: "わ", pianjia: "ワ" },
        { spell: "wo", pingjia: "を", pianjia: "ヲ" },
        { spell: "n", pingjia: "ん", pianjia: "ン" }
      ],

      pingjiaList: [
        "あ",
        "い",
        "う",
        "え",
        "お",
        "か",
        "き",
        "く",
        "け",
        "こ",
        "さ",
        "し",
        "す",
        "せ",
        "そ",
        "た",
        "ち",
        "つ",
        "て",
        "と",
        "な",
        "に",
        "ぬ",
        "ね",
        "の",
        "は",
        "ひ",
        "ふ",
        "へ",
        "ほ",
        "ま",
        "み",
        "む",
        "め",
        "も",
        "や",
        "ゆ",
        "よ",
        "ら",
        "り",
        "る",
        "れ",
        "ろ",
        "わ",
        "を",
        "ん"
      ],

      pianjiaList: [
        "ア",
        "イ",
        "ウ",
        "エ",
        "オ",
        "カ",
        "キ",
        "ク",
        "ケ",
        "コ",
        "サ",
        "シ",
        "ス",
        "セ",
        "ソ",
        "タ",
        "チ",
        "ツ",
        "テ",
        "ト",
        "ナ",
        "ニ",
        "ヌ",
        "ネ",
        "ノ",
        "ハ",
        "ヒ",
        "フ",
        "ヘ",
        "ホ",
        "マ",
        "ミ",
        "ム",
        "メ",
        "モ",
        "ヤ",
        "ユ",
        "ヨ",
        "ラ",
        "リ",
        "ル",
        "レ",
        "ロ",
        "ワ",
        "ヲ",
        "ン"
      ],

      spellList: [
        "a",
        "i",
        "u",
        "e",
        "o",
        "ka",
        "ki",
        "ku",
        "ke",
        "ko",
        "sa",
        "shi",
        "su",
        "se",
        "so",
        "ta",
        "chi",
        "tsu",
        "te",
        "to",
        "na",
        "ni",
        "nu",
        "ne",
        "no",
        "ha",
        "hi",
        "fu",
        "he",
        "ho",
        "ma",
        "mi",
        "mu",
        "me",
        "mo",
        "ya",
        "yu",
        "yo",
        "ra",
        "ri",
        "ru",
        "re",
        "ro",
        "wa",
        "wo",
        "n"
      ]
    };
  },
  methods: {
    keyDown(e) {
      switch (e.keyCode) {
        case 38:
          // 上
          changeCurrIndex(0);
          createWord();
          break;
        case 39:
          // 右
          changeCurrIndex(1);
          createWord();
          break;
        case 40:
          // 下
          changeCurrIndex(2);
          createWord();
          break;
        case 37:
          // 左
          changeCurrIndex(3);
          createWord();
          break;
      }
    },

    changeCurrIndex() {
      let index = 0;
      if (this.mode === 0) {
        switch (this.direct) {
          case 0:
            index =
              this.currIndex === 0
                ? this.wordList.length - 1
                : this.currIndex - 1;
            break;
          case 1:
            index =
              this.currIndex === this.wordList.length - 1
                ? 0
                : this.currIndex + 1;
            break;
          case 2:
            index =
              this.currIndex === this.wordList.length - 1
                ? 0
                : this.currIndex + 1;
            break;
          case 3:
            index =
              this.currIndex === 0
                ? this.wordList.length - 1
                : this.currIndex - 1;
            break;
        }
      }
      if (this.mode === 1) {
        index = this.getRandom(46);
      }
      // if (!this.NewFlag) {
      //   this.currIndex = index;
      // }
      // this.NewFlag = !this.NewFlag;
    },

    createWord() {
      const word = this.wordList[this.currIndex];
      const content = this.NewFlag
        ? word.spell
        : word.spell + " " + word.pingjia + " " + word.pianjia;
      this.show(content);
    },

    show(content) {
      var showDom = document.getElementById("show");
      // showDom.innerHTML = content;
      this.toggleMsg();
    },

    toggleMsg() {
      // const msgDom = document.getElementById("msg");
      // if (msgDom.classList.contains("active")) {
      //   msgDom.classList.remove("active");
      // } else {
      //   msgDom.classList.add("active");
      // }
    },

    switchDirect(type) {
      // 修改查看方式: 0为顺序，1为随机
      // const msgDom = document.getElementById("msg");
      // if (msgDom.classList.contains("active")) {
      //   msgDom.classList.remove("active");
      // }
      this.mode = +type;
      this.currIndex = this.mode === 0 ? 0 : this.getRandom(46);
      this.NewFlag = true;
      this.createWord();
    },
    createSpell() {
      var row = ["a", "i", "u", "e", "o"];
      var col = ["", "k", "s", "t", "n", "h", "m", "y", "r", "w"];
      var list = col.map(val => {
        return row.map(v => {
          return val + v;
        });
      });

      list = list
        .flat()
        .map(v => {
          if (v === "si") return "shi";
          if (v === "ti") return "chi";
          if (v === "tu") return "tsu";
          if (v === "hu") return "fu";
          if (v === "yi") return "";
          if (v === "ye") return "";
          if (v === "wi") return "";
          if (v === "wu") return "";
          if (v === "we") return "";

          return v;
        })
        .filter(v => !!v);
      list.push("nn");

      console.log(list);
      return list;
    },
    getRandom(min, max) {
      if (arguments.length === 1) {
        max = arguments[0];
        min = 0;
      }
      if (arguments.length === 0) {
        return 0;
      }
      return Math.floor(Math.random() * (max - min) + min);
    },

    splitPianjia() {
      var str = `ア (a) カ(ka) サ(sa) タ(ta) ナ(na) ハ(ha) マ(ma)
        イ (i) キ(ki) シ(shi) チ(chi) ニ(ni) ヒ(hi) ミ(mi)
        ウ (u) ク(ku) ス(su) ツ(tsu) ヌ(nu) フ(fu) ム(mu)
        エ (e) ケ(ke) セ(se) テ(te) ネ(ne) ヘ(he) メ(me)
        オ (o) コ(ko) ソ(so) ト(to) ノ(no) ホ(ho) モ(mo)
        ヤ(ya) ワ(wa) ン(n)
        ユ(yu)
        ヨ(yo) ヲ(wo)`;

      var reg = /[\u3040-\u309F\u30A0-\u30FF]/g;
      console.log(str.match(reg));
    },

    createPianjia() {
      var pianjiaList = [
        ["ア", "カ", "サ", "タ", "ナ", "ハ", "マ"],
        ["イ", "キ", "シ", "チ", "ニ", "ヒ", "ミ"],
        ["ウ", "ク", "ス", "ツ", "ヌ", "フ", "ム"],
        ["エ", "ケ", "セ", "テ", "ネ", "ヘ", "メ"],
        ["オ", "コ", "ソ", "ト", "ノ", "ホ", "モ"]
      ];
      var newList = [[], [], [], [], [], [], []];

      for (let i = 0; i < pianjiaList.length; i++) {
        for (let j = 0; j < pianjiaList[0].length; j++) {
          newList[j][i] = pianjiaList[i][j];
        }
      }
      newList = newList.flat();
      newList.push("ヤ");
      newList.push("ユ");
      newList.push("ヨ");
      ["ラ", "リ", "ル", "レ", "ロ"].map(v => {
        newList.push(v);
      });
      newList.push("ワ");
      newList.push("ヲ");
      newList.push("ン");
      return newList;
    },

    createwordList() {
      var newList = [];
      for (let i = 0; i < 46; i += 1) {
        var obj = {
          spell: this.spellList[i],
          pingjia: this.pingjiaList[i],
          pianjia: this.pianjiaList[i]
        };
        newList.push(obj);
      }
      var str = JSON.stringify(newList);
      console.log(str);
      return str;
    }
  },
  mounted() {
    // (function() {
    //   document.onkeydown = this.keyDown();
    //   this.keyDown({
    //     keyCode: 40
    //   });
    // })();
  }
};
</script>
<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
}

#show {
  color: red;
  font-weight: bold;
  font-size: 180px;
  text-align: center;
}
#msg {
  margin-top: 50px;
  color: red;
  font-weight: bold;
  font-size: 90px;
  text-align: center;
}
.active {
  opacity: 0;
}
.btnContainer {
  margin-top: 16px;
  text-align: center;
}
.btn {
  border: none;
  width: 78px;
  height: 32px;
  background: #1890ff;
  color: white;
  margin-right: 16px;
  border-radius: 4px;
  cursor: pointer;
}
</style>

