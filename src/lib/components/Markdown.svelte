<script lang="ts">
	import { Markdown } from '@accuser/svelte-markdown-provider';
	import { mathFromMarkdown } from 'mdast-util-math';
	import { math } from 'micromark-extension-math';
	import type { ComponentProps } from 'svelte';
	import InlineMath from './InlineMath.svelte';
	import Math from './Math.svelte';

	type Props = ComponentProps<Markdown>;

	let { components: _components = {}, directives, options: _options = {}, src }: Props = $props();

	let components = $derived.by(() => ({
		inlineMath: InlineMath,
		math: Math,
		..._components
	}));

	let options = $derived.by(() => ({
		..._options,
		extensions: [...(_options.extensions ?? []), math()],
		mdastExtensions: [...(_options.mdastExtensions ?? []), mathFromMarkdown()]
	}));
</script>

<Markdown {components} {directives} {options} {src} />
