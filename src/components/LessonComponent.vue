<template>
  <v-sheet
    :style="{ width: '50%' }"
    elevation="10"
    class="mx-auto pa-4 mb-4"
  >
    <v-row>
      <v-col cols="12" class="text-center">
        <h3>ターン {{ currentTurn }}</h3>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="4">
        <v-row>
          <v-col>
            <v-btn
              :class="{'selected-button': selectedLesson === 'Vo'}"
              :color="selectedLesson === 'Vo' ? 'grey' : 'pink'"
              @click="selectLesson('Vo')"
            >
              Voレッスン
            </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-btn
              :class="{'selected-button': selectedLesson === 'SP Vo'}"
              :color="selectedLesson === 'SP Vo' ? 'grey' : 'pink'"
              @click="selectLesson('SP Vo')"
            >
              SP Voレッスン
            </v-btn>
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="4">
        <v-row>
          <v-col>
            <v-btn
              :class="{'selected-button': selectedLesson === 'Da'}"
              :color="selectedLesson === 'Da' ? 'grey' : 'cyan'"
              @click="selectLesson('Da')"
            >
              Daレッスン
            </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-btn
              :class="{'selected-button': selectedLesson === 'SP Da'}"
              :color="selectedLesson === 'SP Da' ? 'grey' : 'cyan'"
              @click="selectLesson('SP Da')"
            >
              SP Daレッスン
            </v-btn>
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="4">
        <v-row>
          <v-col>
            <v-btn
              :class="{'selected-button': selectedLesson === 'Vi'}"
              :color="selectedLesson === 'Vi' ? 'grey' : 'yellow'"
              @click="selectLesson('Vi')"
            >
              Viレッスン
            </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-btn
              :class="{'selected-button': selectedLesson === 'SP Vi'}"
              :color="selectedLesson === 'SP Vi' ? 'grey' : 'yellow'"
              @click="selectLesson('SP Vi')"
            >
              SP Viレッスン
            </v-btn>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-sheet>
</template>

<script>
export default {
  props: {
    currentTurn: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      internalData: [
        { lesson: "Vo", value: 10 },
        { lesson: "SP Vo", value: 15 },
        { lesson: "Da", value: 10 },
        { lesson: "SP Da", value: 15 },
        { lesson: "Vi", value: 10 },
        { lesson: "SP Vi", value: 15 }
      ],
      selectedLesson: null,
    };
  },
  methods: {
    selectLesson(lesson) {
      this.selectedLesson = lesson;
      const lessonData = this.internalData.find(data => data.lesson === lesson);
      const increaseValue = lessonData ? lessonData.value : 0;
      this.$emit('lesson-selected', { turn: this.currentTurn, lesson, value: increaseValue });
    },
  }
};
</script>

<style scoped>
.selected-button {
  background-color: grey !important; /* 最後に押されたボタンはグレー */
  color: white !important;
}
.v-btn--pink {
  background-color: pink !important;
  color: black !important;
}
.v-btn--cyan {
  background-color: cyan !important;
  color: black !important;
}
.v-btn--yellow {
  background-color: yellow !important;
  color: black !important;
}
</style>
