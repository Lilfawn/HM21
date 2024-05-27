<template>
  <div class="app">
    <h2 class="base">Base of students</h2>

    <ul>
      <li v-for="student in students" :key="student.id">
        {{ student.name }} - {{ student.score }} points
      </li>
    </ul>

    <p>
      GPA:
      <span :class="averageScoreGroup">
        <span v-if="scoreDirection === 'up'" class="up">↑</span>
        <span v-if="scoreDirection === 'down'" class="down">↓</span>
      </span>
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      students: [],
      previousAverage: 0,
      scoreDirection: null,
    };
  },
  computed: {
    averageScore() {
      if (this.students.length === 0) return 0;
      const total = this.students.reduce((sum, student) => sum + student.score, 0);
      return total / this.students.length;
    },
    averageScoreGroup() {
      if (this.scoreDirection === 'up') {
        return 'orange';
      } else if (this.scoreDirection === 'down') {
        return 'purple';
      } else {
        return '';
      }
    },
  },
  watch: {
    averageScore(newScore, oldScore) {
      if (newScore > oldScore) {
        this.scoreDirection = 'up';
      } else if (newScore < oldScore) {
        this.scoreDirection = 'down';
      }
      this.previousAverage = oldScore;
    },
  },
  methods: {
    generateStudent() {
      let nameList = [
        'Bill','Ann','Kate','Din', 'Bin','Bom','Bam','Bam','Por','Fang', 'Fall','Jmp','Clif',
        'Lin','Ren','Ron','Gessica', 'Steve','Lon','Lam','Alex','De','Pan','Cas', 'Kit','Kin',
        'Obama','Matt','Trooper','Bandit', 'Sam','Lok','Gow','Treck','Deser','Dena','Kyle', 'Mie','Yop',
      ];

      return {
        id: (new Date()).getTime(),
        name: nameList[Math.floor( Math.random() * nameList.length )],
        score: Math.floor( Math.random() * 100)
      };
    },
  },
  created() {
    setInterval(() => {
      this.students.push(this.generateStudent());
    }, 2500)
  }
};
</script>

<style scoped>
.base{
  color: orange;
}
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}

button {
  padding: 8px;
  font-size: 16px;
}


.up {
  color: orange;
}

.down {
  color: purple;
}

</style>
