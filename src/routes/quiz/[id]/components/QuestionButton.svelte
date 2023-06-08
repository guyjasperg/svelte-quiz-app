<script lang="ts">
	export let handleSubmit: () => void;
	export let showCorrectAnswer: boolean;
</script>

<div class="text-center">
	<button class={`bg-blue-900 text-white font-bold p-4 rounded px-16`} on:click={handleSubmit}>
		{#if showCorrectAnswer}
			Next
		{:else}
			Submit
		{/if}
	</button>
</div>
