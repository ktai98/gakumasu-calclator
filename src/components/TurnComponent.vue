<template>
    <v-container>
      <!-- レッスン選択ボタンを含むシート -->
      <v-sheet
        :style="{ width: '50%' }"
        elevation="10"
        class="mx-auto pa-4"
      >
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
  
      <!-- 計算結果の表示 -->
      <v-card v-if="statusIncrease !== null">
        <v-card-title>Calculated Status Increase</v-card-title>
        <v-card-text>{{ statusIncrease }}</v-card-text>
      </v-card>
    </v-container>
  </template>
  
  <script>
  export default {
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
        statusIncrease: null,
      };
    },
    methods: {
      selectLesson(lesson) {
        this.selectedLesson = lesson;
        this.calculateStatusIncrease();
      },
      calculateStatusIncrease() {
        let statusIncrease = 0;
        const lessonData = this.internalData.find(
          (data) => data.lesson === this.selectedLesson
        );
        if (lessonData) {
          statusIncrease = parseInt(lessonData.value, 10);
        }
        this.statusIncrease = statusIncrease;
      },
    },
  };
  </script>
  
  <style>
  .selected-button {
    background-color: grey !important; /* 最後に押されたボタンはグレー */
    color: white !important;
  }
  .v-btn--pink {
    background-color: pink !important;
    color: black !important;
  }
  .v-btn--magenta {
    background-color: magenta !important;
    color: white !important;
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
  