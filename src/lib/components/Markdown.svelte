<script lang="ts">
	import { Markdown } from '@accuser/svelte-markdown-provider';
	import { mathFromMarkdown } from 'mdast-util-math';
	import { math } from 'micromark-extension-math';
	import type { ComponentProps } from 'svelte';
	import InlineMath from './InlineMath.svelte';
	import Math from './Math.svelte';

	type Props = ComponentProps<Markdown>;

	let { ast, components = {}, directives, options = {}, src }: Props = $props();

	let _components = $derived({ inlineMath: InlineMath, math: Math, ...components });

	let _options = $derived.by(() => {
		const { extensions = [], mdastExtensions = [] } = options;

		return {
			extensions: [...extensions, math()],
			mdastExtensions: [...mdastExtensions, mathFromMarkdown()]
		};
	});
</script>

<Markdown {ast} components={_components} {directives} options={_options} {src} />
