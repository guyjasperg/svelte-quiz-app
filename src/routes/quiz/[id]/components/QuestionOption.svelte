<script lang="ts">
	import { select_options } from "svelte/internal";

    export let option: {
        id: number;
        label: string;
        text: string;
    };
    export let selectedOption: null | string;
</script>
<button class="bg-gray-200 rounded w-[49%] text-center p-2 mb-4 py-4"
    on:click={() => selectedOption=option.label}>
    {option.text}
</button>