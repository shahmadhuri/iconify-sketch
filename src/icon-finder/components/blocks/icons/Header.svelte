<script lang="typescript">
	import IconButton from '../../forms/IconButton.svelte';
	import { phrases } from '../../../config/phrases';
	import type { IconsListMode } from '../../types';

	// Text
	export let headerText: string;

	// Mode
	export let isList: boolean;

	// Can toggle mode?
	export let canChangeLayout: boolean;

	// Callback
	export let changeLayout: () => void;

	// Can select multiple icons?
	export let canSelectMultiple: boolean;

	// Selecting icons
	export let isSelecting: boolean;

	// Callback
	export let toggleSelection: () => void;

	// Text
	const text = phrases.icons.header;

	// Modes
	let mode: IconsListMode;
	$: {
		mode = isList ? 'grid' : 'list';
	}

	// Selection icon
	let selectionIcon: string;
	$: {
		selectionIcon = 'check-list' + (isSelecting ? '-checked' : '');
	}
</script>

<div class="iif-icons-header">
	<div class="iif-icons-header-text">{headerText}</div>
	{#if canChangeLayout || canSelectMultiple}
		<div class="iif-icons-header-modes">
			{#if canSelectMultiple}
				<IconButton
					icon={selectionIcon}
					onClick={toggleSelection}
					title={text.select} />
			{/if}
			{#if canChangeLayout}
				{#each [mode] as icon (icon)}
					<IconButton
						{icon}
						onClick={changeLayout}
						title={text.modes[icon]} />
				{/each}
			{/if}
		</div>
	{/if}
</div>
