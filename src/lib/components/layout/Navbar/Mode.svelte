<script lang="ts">
	import { DropdownMenu } from 'bits-ui';
	import { getContext } from 'svelte';

	import { docMode, answers } from '$lib/stores';
	import { flyAndScale } from '$lib/utils/transitions';

	import Dropdown from '$lib/components/common/Dropdown.svelte';

	export let chat;
	const i18n = getContext('i18n');
</script>

<Dropdown>
	<slot />

	<div slot="content">
		<DropdownMenu.Content
			class="w-full max-w-[200px] rounded-xl px-1 py-1.5 border border-gray-300/30 dark:border-gray-700/50 z-50 bg-white dark:bg-gray-850 dark:text-white shadow-lg"
			sideOffset={8}
			side="bottom"
			align="end"
			transition={flyAndScale}
		>
			<DropdownMenu.Item
				class="flex gap-2 items-center px-3 py-2 text-sm  cursor-pointer hover:bg-gray-50 dark:hover:bg-gray-800 rounded-md"
				id="chat-share-button"
				on:click={() => {
					// const messages = $answers.split('\n***\n');
					// for (let i = 0; i < messages.length; i++) {
					// 	chat.chat.messages[2 * i + 1].content = messages[i];
					// 	updateChatById(localStorage.token, chat.chat.messages[2 * i + 1].id, {
					// 		messages: chat.chat.messages,
					// 		history: chat.chat.history,
					// 	});
					// }
					// console.log(chat);
					// console.log(chat.chat.messages);
					// window.location.reload();
					docMode.set(false);
				}}
			>
				<svg width="16px" height="16px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path d="M12 22C17.5228 22 22 17.5228 22 12C22 6.47715 17.5228 2 12 2C6.47715 2 2 6.47715 2 12C2 13.5997 2.37562 15.1116 3.04346 16.4525C3.22094 16.8088 3.28001 17.2161 3.17712 17.6006L2.58151 19.8267C2.32295 20.793 3.20701 21.677 4.17335 21.4185L6.39939 20.8229C6.78393 20.72 7.19121 20.7791 7.54753 20.9565C8.88837 21.6244 10.4003 22 12 22Z" stroke="#1C274C" stroke-width="1.5"/>
					<path opacity="0.5" d="M8 12H8.009M11.991 12H12M15.991 12H16" stroke="#1C274C" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
				</svg>
				<div class="flex items-center">{$i18n.t('Chat Mode')}</div>
			</DropdownMenu.Item>

			<DropdownMenu.Item
				class="flex gap-2 items-center px-3 py-2 text-sm  cursor-pointer hover:bg-gray-50 dark:hover:bg-gray-800 rounded-md"
				id="chat-share-button"
				on:click={() => {
					const messages = chat.chat.messages;
					const messageLength = messages.length;
					const tempDoc = [];
					for (let i = 0; i < messageLength; i++) {
						if (messages[i].role == 'assistant') {
							tempDoc.push(messages[i].content);
						}
					}
					answers.set(tempDoc.join('\n\n') + '\n');
					docMode.set(true);
				}}
			>
				<svg width="16px" height="16px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path d="M4 4C4 3.44772 4.44772 3 5 3H14H14.5858C14.851 3 15.1054 3.10536 15.2929 3.29289L19.7071 7.70711C19.8946 7.89464 20 8.149 20 8.41421V20C20 20.5523 19.5523 21 19 21H5C4.44772 21 4 20.5523 4 20V4Z" stroke="#200E32" stroke-width="2" stroke-linecap="round"/>
					<path d="M20 8H15V3" stroke="#200E32" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
					<path d="M7.5 13H7V17H7.5C8.60457 17 9.5 16.1046 9.5 15C9.5 13.8954 8.60457 13 7.5 13Z" stroke="#200E32" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
					<path d="M17.5 13L17 13C16.4477 13 16 13.4477 16 14V16C16 16.5523 16.4477 17 17 17H17.5" stroke="#200E32" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
					<path d="M11.5 14C11.5 13.4477 11.9477 13 12.5 13H13C13.5523 13 14 13.4477 14 14V16C14 16.5523 13.5523 17 13 17H12.5C11.9477 17 11.5 16.5523 11.5 16V14Z" stroke="#200E32" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
				</svg>
				<div class="flex items-center">{$i18n.t('Doc Mode')}</div>
			</DropdownMenu.Item>

		</DropdownMenu.Content>
	</div>
</Dropdown>
