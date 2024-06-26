<template>
  <v-app>
    <v-main>
      <v-container>
        <!-- ターン管理 -->
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
        <!-- ステータス表示 -->
        <v-row class="mb-4">
          <v-col>
            <v-card>
              <v-card-title>現在ステータス</v-card-title>
              <v-card-text>
                Vo: {{ status.Vo }}<br>
                Da: {{ status.Da }}<br>
                Vi: {{ status.Vi }}
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
        <!-- LessonComponentのリスト -->
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
      status: {
        Vo: 0,
        Da: 0,
        Vi: 0
      },
      lessons: {} // 各ターンのレッスンデータを保存
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
        delete this.lessons[this.currentTurn];
        this.currentTurn -= 1;
        this.calculateTotalStatus();
      }
    },
    handleLessonSelected({ turn, lesson, value }) {
      // 各ターンのレッスンデータを保存
      this.lessons[turn] = { lesson, value };
      this.calculateTotalStatus();
    },
    calculateTotalStatus() {
      // ステータスをリセット
      this.status.Vo = 0;
      this.status.Da = 0;
      this.status.Vi = 0;
      
      // レッスンデータを集計
      for (const key in this.lessons) {
        const lessonData = this.lessons[key];
        if (lessonData.lesson.includes('Vo')) {
          this.status.Vo += lessonData.value;
        } else if (lessonData.lesson.includes('Da')) {
          this.status.Da += lessonData.value;
        } else if (lessonData.lesson.includes('Vi')) {
          this.status.Vi += lessonData.value;
        }
      }
    }
  }
};
</script>

<style>
/* 必要に応じてスタイルを追加してください */
</style>
