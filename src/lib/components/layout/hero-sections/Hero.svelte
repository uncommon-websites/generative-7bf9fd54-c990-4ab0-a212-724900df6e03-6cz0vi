<!--
    @component
    Bold hero banner with eye-catching text and strong call-to-action. NEVER use title case.

    Usage:
    ```html
    <Hero
      title="Bold Claim"
      subtitle="Quick Value"
      imageSrc="https://www.unc.mn/image-placeholder.svg"
      callsToAction={[
        {
          href: "/start",
          label: "Go"
        },
        {
          href: "/learn",
          label: "More"
        }
      ]}
    />
    ```

    Props:
    - `title`: Main headline (string)
    - `subtitle`: Supporting text (string)
    - `imageSrc`: Hero image URL (string)
    - `callsToAction`: CTA buttons array (max two: primary, secondary)
-->

<script lang="ts">
	// Components
	import AnimateText from "$lib/components/animation/AnimateText.svelte";
	import Button from "$lib/components/ui/Button.svelte";

	// Constants
	import { cta } from "$lib/navigation";

	function handleImageError(e: Event) {
		const target = e.currentTarget as HTMLImageElement;
		target.src = "https://placehold.co/1600x900/0b1220/94a3b8?text=\u200B";
	}

	// Types
	type Props = {
		centered?: boolean;
		title: string;
		subtitle: string;
		imageSrc?: string;
		callsToAction?: Array<{
			href: string;
			label: string;
		}>; // A maximum of two calls to action, with the first one being primary and the second one being secondary
		fancy?: boolean; // enables premium visuals
		[key: string]: any;
	};

	let {
		title,
		subtitle,
		imageSrc,
		callsToAction = [cta],
		centered = false,
		fancy = true,
		...rest
	}: Props = $props();
</script>

<div class={["relative isolate overflow-hidden", fancy ? "bg-gradient-to-b from-gray-950 via-gray-950 to-gray-900" : "bg-background"]} {...rest}>
	<!-- radial glow background -->
	{#if fancy}
		<div aria-hidden="true" class="pointer-events-none absolute inset-0 -z-10">
			<div class="absolute left-1/2 top-[-10%] size-[80rem] -translate-x-1/2 rounded-full blur-3xl opacity-40"
				style="background: radial-gradient(closest-side, hsl(222 90% 66% / .35), transparent 70%);"></div>
			<div class="absolute left-[10%] top-[40%] size-[40rem] rounded-full blur-3xl opacity-20"
				style="background: radial-gradient(closest-side, hsl(260 90% 70% / .25), transparent 70%);"></div>
			<div class="absolute right-[-10%] top-[10%] size-[50rem] rounded-full blur-3xl opacity-10"
				style="background: radial-gradient(closest-side, hsl(200 90% 60% / .25), transparent 70%);"></div>
			<div class="absolute inset-0 bg-[radial-gradient(80rem_40rem_at_50%_-20%,hsl(0_0%_100%/.06),transparent)]"></div>
			<div class="absolute inset-0 bg-[linear-gradient(to_bottom,transparent,rgba(0,0,0,.25))]"></div>
		</div>
	{/if}

	<header
		class={[
			"section-px container mx-auto grid items-end gap-10 py-20 pt-28 text-balance",
			centered ? "place-items-center text-center" : " xl:grid-cols-[1fr_auto]"
		]}
		data-enter-container
	>
		<div class="grid gap-6" class:max-w-prose={centered}>
			<!-- Eyebrow -->
			{#if fancy}
				<p class="text-xs md:text-sm inline-flex items-center gap-2 rounded-full border border-white/10 bg-white/5 px-3 py-1 text-white/80 backdrop-blur">
					<span class="relative inline-flex h-2 w-2">
						<span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-primary/70 opacity-75"></span>
						<span class="relative inline-flex h-2 w-2 rounded-full bg-primary"></span>
					</span>
					instant, visual standard work
				</p>
			{/if}

			<h1 class="text-display w-full text-white tracking-tight" data-enter>
				<span class="block"><AnimateText text={title} /></span>
				{#if !centered}
					<span class="text-emphasis-dim block text-white/70"><AnimateText text={subtitle} /></span>
				{/if}
			</h1>

			{#if centered}
				<p
					data-enter
					class=[
						"text-headline mx-auto block max-w-[60ch] text-white/70 transition duration-500 ease-out"
					]
				>
					{subtitle}
				</p>
			{/if}

			{#if callsToAction.length > 0}
				<div class="mt-2 flex gap-3" data-enter>
					{#each callsToAction as cta, index}
						<Button
							href={cta.href}
							size="lg"
							variant={index % 2 === 0 ? "primary" : "secondary"}
							class={[
								"max-lg:hidden",
								index % 2 === 0
									? "shadow-[0_0_0_0_rgba(0,0,0,0)] hover:shadow-[0_10px_30px_-10px_rgba(59,130,246,.5)] transition-shadow"
									: "border-white/30 bg-transparent text-white hover:bg-white/10"
							]}
						>{cta.label}</Button>

						<Button
							href={cta.href}
							size="md"
							variant={index % 2 === 0 ? "primary" : "secondary"}
							class={[
								"lg:hidden",
								index % 2 === 0
									? "shadow-[0_0_0_0_rgba(0,0,0,0)] hover:shadow-[0_10px_30px_-10px_rgba(59,130,246,.5)] transition-shadow"
									: "border-white/30 bg-transparent text-white hover:bg-white/10"
							]}
						>{cta.label}</Button>
					{/each}
				</div>
			{/if}
		</div>

		<!-- Visual panel: glass card or image -->
		<div class="relative hidden xl:block" data-enter>
			<div class="relative w-[640px] rounded-2xl border border-white/10 bg-white/5 p-2 backdrop-blur-md shadow-[inset_0_1px_0_rgba(255,255,255,.06)]">
				<div class="relative overflow-hidden rounded-xl">
					{#if imageSrc}
						<img src={imageSrc} alt="Product visual" class="h-[360px] w-full object-cover" onerror={handleImageError} />
					{:else}
						<div class="h-[360px] w-full bg-[radial-gradient(60rem_30rem_at_50%_-10%,rgba(255,255,255,.15),transparent),linear-gradient(135deg,rgba(255,255,255,.08),rgba(255,255,255,.02))]"></div>
					{/if}
					<!-- glossy highlight -->
					<div aria-hidden class="pointer-events-none absolute inset-x-0 top-0 h-24 bg-gradient-to-b from-white/30 to-transparent"></div>
				</div>
				<!-- base light ring -->
				<div aria-hidden class="pointer-events-none absolute -inset-px rounded-2xl ring-1 ring-white/10"></div>
			</div>
		</div>
	</header>

	{#if imageSrc}
		<!-- Mobile visual below -->
		<div class="col-span-full aspect-video xl:hidden" data-enter>
			<img
				src={imageSrc}
				alt="Product visual"
				class="size-full object-cover"
				onerror={handleImageError}
			/>
		</div>
	{/if}
</div>
