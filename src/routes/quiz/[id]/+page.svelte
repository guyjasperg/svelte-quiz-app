<script lang="ts">
    import QuestionButton from "./components/QuestionButton.svelte";
    import QuestionOption from "./components/QuestionOption.svelte";
    import QuestionText from "./components/QuestionText.svelte";
    import {answers, type Answer} from "../../../store";

    export let data:  any;
    
    let currentQuestionIndex=0;
    let answersValue: Answer[];
    let selectedOption: null | string = null;

    answers.subscribe((value) => {
        answersValue = value;
    })
    $: question = data.questions[currentQuestionIndex];

    const handleNext = () => {
        if(data.questions.length === currentQuestionIndex+1){
            currentQuestionIndex=0;
        }
        else{
            currentQuestionIndex++;
        }        
    }
</script>

<div class="w-full">
    <QuestionText question={question.question} />
    The selected option is {selectedOption}
    <div class="flex justify-between flex-wrap cursor-pointer">
        {#each question.options as option (option.id)}
            <QuestionOption {option} {selectedOption}/>
        {/each}
    </div>
    <QuestionButton/>
    <button type="button" class="bg-indigo-500 ..." disabled>
        <svg class="animate-spin h-5 w-5 mr-3 ..." viewBox="0 0 24 24">
          <!-- ... -->
        </svg>
        Processing...
      </button>
</div>


<style lang="postcss">
    
</style>