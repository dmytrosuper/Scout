<script lang="ts">
	import Bolt from '$lib/components/icons/Bolt.svelte';
	import { onMount, getContext } from 'svelte';

	const i18n = getContext('i18n');

	export let submitPrompt: Function;
	
	export let suggestionPrompts = [];
	
	let prompts = [];

	$: prompts = suggestionPrompts
		.reduce((acc, current) => [...acc, ...[current]], [])
		.sort(() => Math.random() - 0.5);
	// suggestionPrompts.length <= 4
	// 	? suggestionPrompts
	// 	: suggestionPrompts.sort(() => Math.random() - 0.5).slice(0, 4);

	const toggleModal = modalID => {
		document.getElementById(modalID).classList.toggle("hidden");
	}

	onMount(() => {
		const containerElement = document.getElementById('suggestions-container');

		if (containerElement) {
			containerElement.addEventListener('wheel', function (event) {
				if (event.deltaY !== 0) {
					// If scrolling vertically, prevent default behavior
					event.preventDefault();
					// Adjust horizontal scroll position based on vertical scroll
					containerElement.scrollLeft += event.deltaY;
				}
			});
		}
	});
</script>

{#if prompts.length > 0}
	<div class="mb-2 flex gap-1 text-sm font-medium items-center text-gray-400 dark:text-gray-600">
		<Bolt />
		{$i18n.t('Suggested')}
	</div>
{/if}

<div class="w-full">
	<div
		class="relative w-full flex gap-2 snap-x snap-mandatory md:snap-none overflow-x-auto tabs"
		id="suggestions-container"
	>
		<div class="snap-center shrink-0">
			<button
				class="flex flex-col flex-1 shrink-0 w-64 justify-between h-36 p-5 px-6 bg-gray-50 hover:bg-gray-100 dark:bg-gray-850 dark:hover:bg-gray-800 rounded-3xl transition group"
				on:click={() => {
					submitPrompt("Hi! Not sure where to start. How can you help me?");
				}}
			>
				<div class="flex flex-col text-left">
					<!-- {#if prompt.title && prompt.title[0] !== ''} -->
						<div
							class="  font-medium dark:text-gray-300 dark:group-hover:text-gray-200 transition"
						>
						Start Here
							<!-- {prompt.title[0]} -->
						</div>
						<div class="text-sm text-gray-600 font-normal line-clamp-2">Hi! Not sure where to start. How can you help me?</div>
					<!-- {:else}
						<div
							class=" self-center text-sm font-medium dark:text-gray-300 dark:group-hover:text-gray-100 transition line-clamp-2"
						>
							{prompt.content}
						</div>
					{/if} -->
				</div>

				<div class="w-full flex justify-between">
					<div
						class="text-xs text-gray-400 group-hover:text-gray-500 dark:text-gray-600 dark:group-hover:text-gray-500 transition self-center"
					>
						{$i18n.t('Prompt')}
					</div>

					<div
						class="self-end p-1 rounded-lg text-gray-300 group-hover:text-gray-800 dark:text-gray-700 dark:group-hover:text-gray-100 transition"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 16 16"
							fill="currentColor"
							class="size-4"
						>
							<path
								fill-rule="evenodd"
								d="M8 14a.75.75 0 0 1-.75-.75V4.56L4.03 7.78a.75.75 0 0 1-1.06-1.06l4.5-4.5a.75.75 0 0 1 1.06 0l4.5 4.5a.75.75 0 0 1-1.06 1.06L8.75 4.56v8.69A.75.75 0 0 1 8 14Z"
								clip-rule="evenodd"
							/>
						</svg>
					</div>
				</div>
			</button>
		</div>
		<div class="snap-center shrink-0">
			<button
				class="flex flex-col flex-1 shrink-0 w-64 justify-between h-36 p-5 px-6 bg-gray-50 hover:bg-gray-100 dark:bg-gray-850 dark:hover:bg-gray-800 rounded-3xl transition group"
				on:click={() => {
					submitPrompt("How do I decide which roles to hire for first?");
				}}
			>
				<div class="flex flex-col text-left">
					<!-- {#if prompt.title && prompt.title[0] !== ''} -->
						<div
							class="  font-medium dark:text-gray-300 dark:group-hover:text-gray-200 transition"
						>
						Role Prioritization
							<!-- {prompt.title[0]} -->
						</div>
						<div class="text-sm text-gray-600 font-normal line-clamp-2">How do I decide which roles to hire for first?</div>
					<!-- {:else}
						<div
							class=" self-center text-sm font-medium dark:text-gray-300 dark:group-hover:text-gray-100 transition line-clamp-2"
						>
							{prompt.content}
						</div>
					{/if} -->
				</div>

				<div class="w-full flex justify-between">
					<div
						class="text-xs text-gray-400 group-hover:text-gray-500 dark:text-gray-600 dark:group-hover:text-gray-500 transition self-center"
					>
						{$i18n.t('Prompt')}
					</div>

					<div
						class="self-end p-1 rounded-lg text-gray-300 group-hover:text-gray-800 dark:text-gray-700 dark:group-hover:text-gray-100 transition"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 16 16"
							fill="currentColor"
							class="size-4"
						>
							<path
								fill-rule="evenodd"
								d="M8 14a.75.75 0 0 1-.75-.75V4.56L4.03 7.78a.75.75 0 0 1-1.06-1.06l4.5-4.5a.75.75 0 0 1 1.06 0l4.5 4.5a.75.75 0 0 1-1.06 1.06L8.75 4.56v8.69A.75.75 0 0 1 8 14Z"
								clip-rule="evenodd"
							/>
						</svg>
					</div>
				</div>
			</button>
		</div>
		<div class="snap-center shrink-0">
			<button
				class="flex flex-col flex-1 shrink-0 w-64 justify-between h-36 p-5 px-6 bg-gray-50 hover:bg-gray-100 dark:bg-gray-850 dark:hover:bg-gray-800 rounded-3xl transition group"
				on:click={() => {
					submitPrompt("What should my team structure look like?");
				}}
			>
				<div class="flex flex-col text-left">
					<!-- {#if prompt.title && prompt.title[0] !== ''} -->
						<div
							class="  font-medium dark:text-gray-300 dark:group-hover:text-gray-200 transition"
						>
						Team Structure
							<!-- {prompt.title[0]} -->
						</div>
						<div class="text-sm text-gray-600 font-normal line-clamp-2">What should my team structure look like?</div>
					<!-- {:else}
						<div
							class=" self-center text-sm font-medium dark:text-gray-300 dark:group-hover:text-gray-100 transition line-clamp-2"
						>
							{prompt.content}
						</div>
					{/if} -->
				</div>

				<div class="w-full flex justify-between">
					<div
						class="text-xs text-gray-400 group-hover:text-gray-500 dark:text-gray-600 dark:group-hover:text-gray-500 transition self-center"
					>
						{$i18n.t('Prompt')}
					</div>

					<div
						class="self-end p-1 rounded-lg text-gray-300 group-hover:text-gray-800 dark:text-gray-700 dark:group-hover:text-gray-100 transition"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 16 16"
							fill="currentColor"
							class="size-4"
						>
							<path
								fill-rule="evenodd"
								d="M8 14a.75.75 0 0 1-.75-.75V4.56L4.03 7.78a.75.75 0 0 1-1.06-1.06l4.5-4.5a.75.75 0 0 1 1.06 0l4.5 4.5a.75.75 0 0 1-1.06 1.06L8.75 4.56v8.69A.75.75 0 0 1 8 14Z"
								clip-rule="evenodd"
							/>
						</svg>
					</div>
				</div>
			</button>
		</div>
		<div class="snap-center shrink-0">
			<button
				class="flex flex-col flex-1 shrink-0 w-64 justify-between h-36 p-5 px-6 bg-gray-50 hover:bg-gray-100 dark:bg-gray-850 dark:hover:bg-gray-800 rounded-3xl transition group"
				on:click={() => {
					toggleModal("meetings");
				}}
			>
				<div class="flex flex-col text-left">
					<!-- {#if prompt.title && prompt.title[0] !== ''} -->
						<div
							class="  font-medium dark:text-gray-300 dark:group-hover:text-gray-200 transition"
						>
						Talk to a Human
							<!-- {prompt.title[0]} -->
						</div>
						<div class="text-sm text-gray-600 font-normal line-clamp-2">I’d like to book a meeting with a Satori consultant.</div>
					<!-- {:else}
						<div
							class=" self-center text-sm font-medium dark:text-gray-300 dark:group-hover:text-gray-100 transition line-clamp-2"
						>
							{prompt.content}
						</div>
					{/if} -->
				</div>

			</button>
		</div>
		<!-- {#each prompts as prompt, promptIdx}
			<div class="snap-center shrink-0">
				<button
					class="flex flex-col flex-1 shrink-0 w-64 justify-between h-36 p-5 px-6 bg-gray-50 hover:bg-gray-100 dark:bg-gray-850 dark:hover:bg-gray-800 rounded-3xl transition group"
					on:click={() => {
						submitPrompt(prompt.content);
					}}
				>
					<div class="flex flex-col text-left">
						{#if prompt.title && prompt.title[0] !== ''}
							<div
								class="  font-medium dark:text-gray-300 dark:group-hover:text-gray-200 transition"
							>
								{prompt.title[0]}
							</div>
							<div class="text-sm text-gray-600 font-normal line-clamp-2">{prompt.title[1]}</div>
						{:else}
							<div
								class=" self-center text-sm font-medium dark:text-gray-300 dark:group-hover:text-gray-100 transition line-clamp-2"
							>
								{prompt.content}
							</div>
						{/if}
					</div>

					<div class="w-full flex justify-between">
						<div
							class="text-xs text-gray-400 group-hover:text-gray-500 dark:text-gray-600 dark:group-hover:text-gray-500 transition self-center"
						>
							{$i18n.t('Prompt')}
						</div>

						<div
							class="self-end p-1 rounded-lg text-gray-300 group-hover:text-gray-800 dark:text-gray-700 dark:group-hover:text-gray-100 transition"
						>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								viewBox="0 0 16 16"
								fill="currentColor"
								class="size-4"
							>
								<path
									fill-rule="evenodd"
									d="M8 14a.75.75 0 0 1-.75-.75V4.56L4.03 7.78a.75.75 0 0 1-1.06-1.06l4.5-4.5a.75.75 0 0 1 1.06 0l4.5 4.5a.75.75 0 0 1-1.06 1.06L8.75 4.56v8.69A.75.75 0 0 1 8 14Z"
									clip-rule="evenodd"
								/>
							</svg>
						</div>
					</div>
				</button>
			</div>
		{/each} -->

		<!-- <div class="snap-center shrink-0">
		<img
			class="shrink-0 w-80 h-40 rounded-lg shadow-xl bg-white"
			src="https://images.unsplash.com/photo-1604999565976-8913ad2ddb7c?ixlib=rb-1.2.1&amp;ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&amp;auto=format&amp;fit=crop&amp;w=320&amp;h=160&amp;q=80"
		/>
	</div> -->
	</div>
	<div id="meetings" class="fixed inset-0 flex items-center justify-center z-50 hidden bg-black bg-opacity-50">
		<div class="bg-white rounded-lg shadow-lg w-4/5 h-full flex flex-col">
			<div class="flex justify-between items-center p-4 border-b">
				<h2 class="text-xl font-semibold">Meeting with Satori</h2>
				<button class="text-black" on:click={() => {
					toggleModal("meetings");
				}}>&times;</button>
			</div>
			<div class="flex-grow">
				<!-- Iframe -->
				<iframe class="w-full h-full" src="https://calendly.com/dmytrov62/30min" frameborder="0" allowfullscreen></iframe>
			</div>
			<div class="flex justify-end p-4 border-t">
				<button class="bg-gray-500 text-white font-bold py-2 px-4 rounded" on:click={() => {
					toggleModal("meetings");
				}}>Close</button>
			</div>
		</div>
	</div>
</div>

<style>
	.tabs::-webkit-scrollbar {
		display: none; /* for Chrome, Safari and Opera */
	}

	.tabs {
		-ms-overflow-style: none; /* IE and Edge */
		scrollbar-width: none; /* Firefox */
	}
</style>
