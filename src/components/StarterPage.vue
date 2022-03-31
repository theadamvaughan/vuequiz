<template>
  <div class="questions-ctr">
    <div class="single-question">
      <div class="question">Do You Want To Start The Quiz?</div>
      <div class="answers">
        <div
        @click.prevent="startedQuiz()"
        >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    props: [""],
    emits: ["startQuiz"],
    methods: {
        startingQuiz() {
          this.$emit("startQuiz")
        } 
      }
    };
</script>
