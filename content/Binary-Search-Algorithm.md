Title: Binary Search Algorithm
Description: The Secret to Effective and Fast Search
Date: 2025-01-22 20:00
Tags: Algorithm


### Binary Search Algorithm 
Hi! I'll tell you binary search algorithm and show an example in today  
### İntroduction
Algorithms are one of the cornerstones of software development, and the binary search algorithm is one of the most used algorithms thanks to its efficiency and fast performance.

### Binary Search and Git

Git is a distributed version control system used to manage software projects. The binary search algorithm is used to help Git find errors in a commit history.

The git bisect command in Git works based on the binary search algorithm to find in which commit an error started.

## Popularity

**Binary Search** algorithm is one of the first algorithms that come to mind when it comes to search algorithm.

<img src="https://i.redd.it/d0olgpdxogy91.jpg" alt="Sample Image" width="500">

## Example 
The sample was taken from [this address](https://github.com/abdullah/paradoks), thank you Abdullah 

<html>

<head>
  <script src="//unpkg.com/vue@2"></script>
  <link href="https://fonts.googleapis.com/css?family=Raleway" rel="stylesheet">
  <style id="extra-rule">
.home div{
  padding: 0;
  margin: 0;
  font-family: "Raleway", sans-serif;
  background-color: var(--dark-color);
  background-size: 400% 400%;
  color: var(--light-color);
  --dark-color: #0d1120;
  --light-color: #ceec4c;
  --border-radius: 20px;
}
nav {
  position: sticky;
  top: 0;
  display: flex;
  width: 100%;
  background-color: var(--dark-color);
  padding: 10px;
  align-items: center;
  box-sizing: border-box;
  border-bottom: 1px solid var(--light-color);
}
nav p {
  flex: 1;
}
nav p small {
  display: flex;
  align-items: center;
}
nav input {
  border: 0;
  font-size: 23px;
  text-align: center;
  width: 100px;
  border-bottom: 1px solid var(--light-color);
  background-color: transparent;
  color: var(--light-color);
}
nav button {
  padding: 10px 20px;
  border: 0;
  margin: 0 10px;
  color: var(--dark-color);
  background-color: var(--light-color);
  font-weight: bold;
  font-size: 20px;
  cursor: pointer;
  border-radius: 10px;
}
.steps-indicator {
  background-color: var(--light-color);
  color: var(--dark-color);
  padding: 10px;
  display: inline-flex;
  align-items: center;
}
.steps-indicator b {
  font-size: 30px;
  margin-right: 10px;
}
.card {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 20px;
}
.card span {
  width: 60px;
  height: 60px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  border: 1px solid var(--light-color);
  border-radius: var(--border-radius);
  transition: all 1s;
  margin: 10px;
  font-size: 20px;
}
.result {
  padding: 20px;
  text-align: center;
  animation: bounce-in 0.6s;
  max-width: 300px;
  margin: auto auto;
}
.result p {
  margin: 0;
  padding: 0;
}
.result h1 {
  margin: 0 0 10px 0;
  padding: 10px 0;
  border-bottom: 1px solid var(--light-color);
}
.result a {
  text-decoration: none;
  margin: 15px;
  color: var(--light-color);
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
</style>
</head>

<body>
<div class="home div">
  <div id="paradoks">
    <div v-show="step !== totalStep">
      <nav>
        <p>
          Choose a number between 1 and
          <input v-model="maxSizeInput" type="text">
          If you have a number on the screen press
          <button @click="yep">
            Yep
          </button>
          or
          <button @click="nope">
            Nope
          </button>
          <small>Press a number on your keyboard to highlight numbers which start with it.</small>
        </p>
<div class="steps-indicator">
          <b>{{ totalStep - step }}</b> steps remaining
        </div>
      </nav>

<div class="card">
        <span v-for="p in currentCard" :key="p" :class="p.toString()">{{ p }}</span>
      </div>
    </div>

<div v-if="step === totalStep" class="result">
      <h1>{{ resultText }}</h1>
      <a href="" @click.prevent="reset">Try again</a>
    </div>
  </div>
</div>

  <script>new Vue({
  el: '#paradoks',
  data() {
    return {
      step: 0,
      result: 0,
      maxSize: 2048,
      maxSizeInput: 2048
    };
  },
  computed: {
    totalStep() {
      return Math.ceil(Math.log2(this.maxSize));
    },
    paradoks() {
      const paradoks = [];
      let loop = true;
      let grupSize = 1;
      let cardSize = 0;
      let next = false;
      let maxLimit = 0;

      while (loop) {
        paradoks[cardSize] = [];

        for (let i = grupSize; i <= this.maxSize; i++) {
          if (i % grupSize == 0) {
            next = !next;
          }

          if (next) {
            paradoks[cardSize].push(i);
          }
        }

        cardSize++;
        grupSize *= 2;
        next = false;
        if (cardSize == this.totalStep) {
          loop = false;
        }
      }

      return paradoks;
    },
    currentCard() {
      return this.paradoks[this.step];
    },
    resultText() {
      if (this.result > 0 && this.result) {
        return `😎😎 ${this.result} 😎😎`;
      }
      return `Whoops! '${this.result}' is found.`;

    }
  },
  watch: {
    maxSizeInput(value) {
      if (value > 3) {

        if (value > 5000) {
          const res = confirm('Are you sure you want to render more than 5000?');
          if (!res) {
            return;
          }
        }

        this.maxSize = value;
        this.reset();
      }
    }
  },
  mounted() {
    const extraRuleTag = document.querySelector('#extra-rule');
    document.addEventListener('keydown', (e) => {
      if (Number.isSafeInteger(parseInt(e.key))) {
        extraRuleTag.innerHTML = `[class^="${e.key}"] { background-color: red }`
      }
    })
  },
  methods: {
    yep() {
      this.result += this.paradoks[this.step][0];
      this.step++;
    },
    nope() {
      this.step++;
    },
    reset() {
      this.step = 0;
      this.result = 0;
    }
  }
});</script>
</body>

</html>
