<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row class="mb-4">
          <v-col>
            <v-btn @click="decreaseTurn">ターン削除</v-btn>
          </v-col>
          <v-col>
            <v-btn @click="increaseTurn">ターン追加</v-btn>
          </v-col>
          <v-col>
            <v-chip>{{ currentTurn }}</v-chip>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <div v-for="turn in turns" :key="turn">
              <lesson-component
                :currentTurn="turn"
                @lesson-selected="handleLessonSelected"
              ></lesson-component>
            </div>
          </v-col>
        </v-row>
        <!-- 計算結果の表示 -->
        <v-card v-if="statusIncrease !== null">
          <v-card-title>Calculated Status Increase</v-card-title>
          <v-card-text>
            レッスン: {{ selectedLesson }}<br>
            上昇値: {{ statusIncrease }}
          </v-card-text>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import LessonComponent from './components/LessonComponent.vue';

export default {
  components: {
    LessonComponent,
  },
  data() {
    return {
      currentTurn: 1,
      turns: [1], // 初期のターンは1
      selectedLesson: null,
      statusIncrease: null,
    };
  },
  methods: {
    increaseTurn() {
      this.currentTurn += 1;
      this.turns.push(this.currentTurn);
    },
    decreaseTurn() {
      if (this.currentTurn > 1) {
        this.turns.pop();
        this.currentTurn -= 1;
      }
    },
    handleLessonSelected({ lesson, value }) {
      this.selectedLesson = lesson;
      this.statusIncrease = value;
    },
  },
};
</script>

<style>
/* 必要に応じてスタイルを追加してください */
</style>
