# Svelte Markdown Provider

A [Svelte 5](https://svelte-5-preview.vercel.app/docs/introduction) component for rendering Markdown with [Math](https://github.com/syntax-tree/mdast-util-math/) as components with fine-grained reactivity.

## Example

- [Math](math)

## Installation

```bash
# or yarn, or pnpm
npm install --save @accuser/svelte-markdown-math
```

## Usage

```svelte
<script>
  import Markdown from '@accuser/svelte-markdown-math';
</script>

<Markdown>
  # Hello, world!
</Markdown>
```
