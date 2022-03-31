/* eslint-disable vue/multi-word-component-names */
<template>
  <div class="ctr">
    <!-- set startedQuiz under data to true to skip starter page -->
    <starter v-if="startedQuiz==false"
    @startQuiz="startedQuiz"
    />
    <!-- If the number of questions answered is less than the number of questions available, show the questions component, otherwise show results -->
    <questions v-else-if="questionsAnswered < questions.length" 
    :questions="questions"
    :questionsAnswered="questionsAnswered"
    @question-answered="questionAnswered"
    />
    <result v-else :results="results" :totalCorrect="totalCorrect" :totalQuestions="questionsAnswered"/>
    <div>
      <button 
      type="button" 
      class="reset-btn" 
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
      >
      Reset
      </button>
      <button v-if="startedQuiz == false" type="button" class="start-btn" @click.prevent="startQuiz">Yes!</button>
    </div>
  </div>
</template>

<script>
import Questions from './components/QuestionsTemplate.vue'
import Result from './components/ResultTemplate.vue'
import Starter from './components/StarterPage.vue'

export default {
  name: 'App',
  components: {
    Starter,
    Questions, 
    Result,
  },
  data() {
    return {
      startedQuiz: false,
      questionsAnswered: 0,
      totalCorrect:0, 
      questions: [
        {
          q: 'Who does Tom Cruise play in Top Gun?', 
          answers: [
            {
              text: 'Maverick',
              is_correct: true
            },
            {
              text: 'Iceman',
              is_correct: false 
            },
            {
              text: 'Goose',
              is_correct: false 
            },
            {
              text: 'Viper',
              is_correct: false 
            }
            ] 
        },
        { 
          q: 'In Anchorman, what’s the name of Ron Burgundy’s dog?', 
          answers: [
            {
              text: 'Bingo',
              is_correct: false
            },
            {
              text: 'Barkley',
              is_correct: false 
            },
            {
              text: 'Baxter',
              is_correct: true 
            },
            {
              text: 'Brutus',
              is_correct: false 
            }
          ] 
        },
        { 
          q: 'In The Matrix, does Neo take the blue pill or the red pill?', 
          answers: [
            {
              text: 'Red pill',
              is_correct: true
            },
            {
              text: 'Blue pill',
              is_correct: false 
            }
        ]   
        },
        { 
          q: 'In the film WALL-E, What does WALL-E stand for?', 
          answers: [
            {
              text: 'World Administration Life Locator Electrical',
              is_correct: false
            },
            {
              text: 'Waste Alien Location Lever Electrifier',
              is_correct: false 
            },
            {
              text: 'Weird Aliens Love Laughing at Earth',
              is_correct: false
            },
            {
              text: 'Waste Allocation Load-Lifter: Earth-Class',
              is_correct: true
            }
        ]   
        },
        { 
          q: 'In the film Wreck-it Ralph, which game does Wreck-It Ralph appear in?', 
          answers: [
            {
              text: 'Fix-it Frank Jr.',
              is_correct: false
            },
            {
              text: 'Fix-it Felix, Jr.',
              is_correct: true 
            },
            {
              text: 'Fix-it Fred, Jr.',
              is_correct: false 
            },
            {
              text: 'Fix-it Fernando, Jr.',
              is_correct: false 
            }
        ]   
        },
        { 
          q: 'In Apocalypse Now, Robert Duvall says, “I love the smell of _____ in the morning.”', 
          answers: [
            {
              text: 'Breakfast',
              is_correct: false
            },
            {
              text: 'Gunfire',
              is_correct: false 
            },
            {
              text: 'Coffee',
              is_correct: false 
            },
            {
              text: 'Napalm',
              is_correct: true
            }
        ]   
        },
        { 
          q: 'Which American director won an oscar for helming Forrest Gump?', 
          answers: [
            {
              text: 'Stephen Spielberg',
              is_correct: false
            },
            {
              text: 'Robert Zemeckis',
              is_correct: true 
            },
            {
              text: 'Ron Howard',
              is_correct: false 
            },
            {
              text: 'Robert Altman',
              is_correct: false 
            }
        ]   
        },
        { 
          q: 'What’s the fictional brand of cigarettes in Quentin Tarantinoçs movies?', 
          answers: [
            {
              text: 'Red Apple cigarettes',
              is_correct: true
            },
            {
              text: 'Red Maple cigarettes',
              is_correct: false 
            },
            {
              text: 'Red Camel cigarettes',
              is_correct: false 
            },
            {
              text: 'Red Cowboy cigarettes',
              is_correct: false 
            }
        ]   
        },
        { 
          q: 'Which actor played Linus Caldwell in the Ocean’s film trilogy?', 
          answers: [
            {
              text: 'Brad Pitt',
              is_correct: false
            },
            {
              text: 'George Clooney',
              is_correct: false 
            },
            {
              text: 'Casey Affleck',
              is_correct: false 
            },
            {
              text: 'Matt Damon',
              is_correct: true 
            }
        ]   
        },
        { 
          q: 'In Ghostbusters, how much does Ray Stantz pay for the car Ecto-1 is based off?', 
          answers: [
            {
              text: '$5000',
              is_correct: false
            },
            {
              text: '$5600',
              is_correct: false 
            },
            {
              text: '$4800',
              is_correct: true 
            },
            {
              text: '$6500',
              is_correct: false 
            }
        ]   
        },
      ],
      results: [
        {
          min: 0,
          max: 3,
          title: "Woeful!",
          desc: "You need to watch more films!"
        },
        {
          min: 4,
          max: 6,
          title: "Room for improvement!",
          desc: "Don't cancel that Netflix subscription just yet!"
        },
        {
          min: 7,
          max: 9,
          title: "Great job!",
          desc: "Watch a few more films and you'll get top marks!"
        },
        {
          min: 10,
          max: 10,
          title: "Wow, you're a genius!",
          desc: "What you don't know about films isn't worth knowing!"
        },
      ],
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if(is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    startQuiz() {
      this.startedQuiz = true;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    }
  },
};
</script>