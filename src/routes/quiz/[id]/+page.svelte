<script lang="ts">
	import QuestionButton from './components/QuestionButton.svelte';
	import QuestionOption from './components/QuestionOption.svelte';
	import QuestionText from './components/QuestionText.svelte';
	import { answers, type Answer } from '../../../store';
	import { onMount } from 'svelte';
	import QuestionProgressCircle from './components/QuestionProgressCircle.svelte';

	export let data: any;

	let currentQuestionIndex = 0;
	let answersValue: Answer[];
	let selectedOption: null | string = null;
	let showCorrectAnswer: boolean = false;

	answers.subscribe((value) => {
		answersValue = value;
	});
	$: question = data.questions[currentQuestionIndex];

	const handleNext = () => {
		if (data.questions.length === currentQuestionIndex + 1) {
			currentQuestionIndex = 0;
		} else {
			currentQuestionIndex++;
		}
	};

	const handleSubmit = () => {
		if (!selectedOption) return;
		if (showCorrectAnswer) {
			showCorrectAnswer = false;
			selectedOption = null;
			currentQuestionIndex++;
			return;
		}
		//evaluate if answer selected is correct
		showCorrectAnswer = true;
		answers.update((value) => {
			const updatedAnswerState = value;
			updatedAnswerState[currentQuestionIndex].isCorrect = selectedOption === question.answer;
			return updatedAnswerState;
		});
	};

	const handleChangeOption = (label: string) => {
		selectedOption = label;
		console.log('handleChangeOption', label);
	};

	onMount(() => {
		answers.set(
			data.questions.map((question: any) => {
				return {
					id: question.id,
					isCorrect: null
				};
			})
		);
	});
</script>

<div class="w-full">
	<div class="flex justify-center">
		{#each answersValue as answer}
			<QuestionProgressCircle isCorrect={answer.isCorrect} />
		{/each}
	</div>
	<QuestionText question={question.question} />
	<div class="flex justify-between flex-wrap cursor-pointer">
		{#each question.options as option (option.id)}
			<QuestionOption
				{option}
				{selectedOption}
				{showCorrectAnswer}
				answer={question.answer}
				{handleChangeOption}
			/>
		{/each}
	</div>
	<QuestionButton {handleSubmit} {showCorrectAnswer} />
</div>
