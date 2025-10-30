<script lang="ts" module>
	import type { Snippet } from 'svelte';
	import { tv, type VariantProps } from 'tailwind-variants';

	import { cn, type WithElementRef } from '$lib/utils';

	export const typographyVariants = tv({
		defaultVariants: {
			variant: 'p',
		},
		variants: {
			variant: {
				blockquote: 'mt-6 border-l-2 pl-6 italic',
				code: 'bg-muted relative rounded px-[0.3rem] py-[0.2rem] font-mono text-sm font-semibold',
				h1: 'scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl',
				h2: 'scroll-m-20 border-b pb-2 text-3xl font-semibold tracking-tight transition-colors first:mt-0',
				h3: 'scroll-m-20 text-2xl font-semibold tracking-tight',
				h4: 'scroll-m-20 text-xl font-semibold tracking-tight',
				large: 'text-lg font-semibold',
				lead: 'text-muted-foreground text-xl',
				muted: 'text-muted-foreground text-sm',
				p: 'leading-7 [&:not(:first-child)]:mt-6',
				small: 'text-sm font-medium leading-none',
			},
		},
	});
	export type TypographyVariant = VariantProps<typeof typographyVariants>['variant'];
	export type TypographyProps = WithElementRef<HTMLElement> & {
		variant?: TypographyVariant;
		class?: string;
		children: Snippet<[]>;
	};
</script>

<script lang="ts">
	let { children, variant, class: className, ref = $bindable(null) }: TypographyProps = $props();
	let componentClass = cn(typographyVariants({ variant }), className);
</script>

{#if variant === 'blockquote'}
	<blockquote class={componentClass} bind:this={ref}>
		{@render children?.()}
	</blockquote>
{:else if variant === 'code'}
	<code class={componentClass} bind:this={ref}>{@render children?.()}</code>
{:else if variant === 'h1'}
	<h1 class={componentClass} bind:this={ref}>{@render children?.()}</h1>
{:else if variant === 'h2'}
	<h2 class={componentClass} bind:this={ref}>{@render children?.()}</h2>
{:else if variant === 'h3'}
	<h3 class={componentClass} bind:this={ref}>{@render children?.()}</h3>
{:else if variant === 'h4'}
	<h4 class={componentClass} bind:this={ref}>{@render children?.()}</h4>
{:else if variant === 'small'}
	<small class={componentClass} bind:this={ref}>{@render children?.()}</small>
{:else}
	<p class={componentClass} bind:this={ref}>{@render children?.()}</p>
{/if}
