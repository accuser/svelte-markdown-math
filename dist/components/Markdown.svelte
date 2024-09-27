<script lang="ts">
	import { Markdown } from '@accuser/svelte-markdown-provider';
	import { mathFromMarkdown } from 'mdast-util-math';
	import { math } from 'micromark-extension-math';
	import type { ComponentProps } from 'svelte';
	import InlineMath from './InlineMath.svelte';
	import Math from './Math.svelte';

	type Props = ComponentProps<Markdown>;

	let { ast, components: _components, directives, options: _options, src }: Props = $props();

	let components = $derived.by(() => {
		const { ...rest } = _components ?? {};

		return {
			inlineMath: InlineMath,
			math: Math,
			...rest
		};
	});

	let options = $derived.by(() => {
		const { extensions = [], mdastExtensions = [], ...rest } = _options ?? {};

		return {
			extensions: [...extensions, math()],
			mdastExtensions: [...mdastExtensions, mathFromMarkdown()],
			...rest
		};
	});
</script>

<Markdown {ast} {components} {directives} {options} {src} />
