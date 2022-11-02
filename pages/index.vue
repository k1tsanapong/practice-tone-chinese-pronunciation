<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="7">
      <v-card class="logo my-16 py-4 d-flex justify-center">
        <div class="transition-swing text-h1" v-text="got"></div>
      </v-card>
    </v-col>

    <v-col cols="12" sm="12" md="12" class="py-4 d-flex justify-center">
      <v-card>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            large
            nuxt
            @click="play(randomWord(), randomTone())"
          >
            Random
          </v-btn>
        </v-card-actions>

        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" large nuxt @click="play(got_word, got_tone)">
            Again
          </v-btn>
        </v-card-actions>

        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" large nuxt @click="play(got_word, plusTone())">
            Plus
          </v-btn>
        </v-card-actions>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            large
            nuxt
            @click="play(got_word, minusTone())"
          >
            Battle
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import data from "raw-loader!../static/words_2.txt";

export default {
  name: "IndexPage",

  data() {
    return {
      got: "Just a Word",
      got_word: "-1",
      got_tone: "-1",
    };
  },
  beforeCreate() {},
  created() {
    //  this.play();
  },

  methods: {
    randomWord() {
      const myArray = data.split(",");
      let num = Math.floor(Math.random() * 408);
      let word = myArray[num];
      this.got_word = word;
      return word;
    },

    randomTone() {
      let tone = Math.floor(Math.random() * 4) + 1;
      this.got_tone = tone;
      return tone;
    },

    play(word, tone) {
      this.got = word + " " + tone;

      let sound =
        "https://yabla.vo.llnwd.net/media.yabla.com/chinese_static/audio/alicia/" +
        word +
        tone +
        ".mp3";
      let audio = new Audio(sound);
      audio.play();
    },

    plusTone() {
      if (this.got_tone >= 4) {
        this.got_tone = 1;
        return 1;
      }

      return (this.got_tone = this.got_tone + 1);
    },
    minusTone() {
      if (this.got_tone <= 1) {
        this.got_tone = 4;
        return 4;
      }

      return (this.got_tone = this.got_tone - 1);
    },
  },
  beforeMount() {},
};
</script>
