<script lang="ts">
  import Nav from "$lib/components/layout/Nav.svelte";
  import Hero from "$lib/components/layout/hero-sections/Hero.svelte";
  import LogoScroller from "$lib/components/layout/LogoScroller.svelte";
  import Features from "$lib/components/layout/Features.svelte";
  import Stats from "$lib/components/layout/Stats.svelte";
  import Testimonials from "$lib/components/layout/Testimonials.svelte";
  import CallToAction from "$lib/components/layout/CallToAction.svelte";
  import Footer from "$lib/components/layout/Footer.svelte";

  // Icons
  import IconCamera from "~icons/lucide/camera";
  import IconSearch from "~icons/lucide/search";
  import IconClock from "~icons/lucide/clock";
  import IconShield from "~icons/lucide/shield";
  import IconWifiOff from "~icons/lucide/wifi-off";
  import IconCheckCircle from "~icons/lucide/check-circle";

  const hero = {
    title: "no more bottlenecks when your experts are out",
    subtitle:
      "capture tribal knowledge as it happens. squint turns everyday workflows into searchable visual instructions in seconds.",
    callsToAction: [
      { href: "/demo", label: "Book a demo" },
      { href: "/overview", label: "Watch 60-sec overview" }
    ]
  };

  const logoUrls = [
    "https://cdn.brandfetch.io/brand/logos/placeholder-1",
    "https://cdn.brandfetch.io/brand/logos/placeholder-2",
    "https://cdn.brandfetch.io/brand/logos/placeholder-3",
    "https://cdn.brandfetch.io/brand/logos/placeholder-4",
    "https://cdn.brandfetch.io/brand/logos/placeholder-5",
    "https://cdn.brandfetch.io/brand/logos/placeholder-6"
  ];

  const howItWorks = [
    {
      title: "capture while you work",
      description:
        "record the process with voice and visuals—no writing or templates.",
      icon: IconCamera
    },
    {
      title: "auto organize and index",
      description: "squint turns captures into step-by-step guides you can search.",
      icon: IconSearch
    },
    {
      title: "share and standardize",
      description: "publish approved instructions so anyone can run the job right.",
      icon: IconCheckCircle
    }
  ];

  const features = [
    {
      title: "visual-first instructions",
      description: "show, don’t tell—clear steps with voice and images for faster ramp.",
      icon: IconCamera
    },
    {
      title: "instant search",
      description: "find steps by part, machine, or keyword in seconds.",
      icon: IconSearch
    },
    {
      title: "works offline",
      description: "reliable on noisy floors and low connectivity sites.",
      icon: IconWifiOff
    },
    {
      title: "access control",
      description: "set who can capture, edit, and approve instructions.",
      icon: IconShield
    },
    {
      title: "faster onboarding",
      description: "typical teams cut training time by up to 50%.",
      icon: IconClock
    },
    {
      title: "version history",
      description: "see what changed and when to keep standards tight.",
      icon: IconCheckCircle
    }
  ];

  const stats = [
    { value: "50%", description: "typical reduction in ramp time", icon: IconClock },
    { value: "+12%", description: "typical lift in first-pass yield", icon: IconCheckCircle },
    { value: "-20%", description: "typical cut in unplanned downtime", icon: IconShield }
  ];

  const testimonials = [
    {
      name: "Alex Romero",
      position: "operations manager",
      company: "Midwest Components",
      quote:
        "squint finally got our process out of people’s heads. new hires follow the same steps from day one, and we don’t stall when a veteran is off shift.",
      image:
        "https://images.unsplash.com/photo-1544717305-2782549b5136?w=600&h=800&fit=crop&auto=format"
    }
  ];

  const comparison = [
    {
      title: "why not notion or confluence?",
      points: [
        "writing-heavy; floor teams won’t maintain pages",
        "no instant capture while doing the job",
        "less effective on mobile and noisy environments"
      ]
    },
    {
      title: "why not guru or slab?",
      points: [
        "optimized for office knowledge, not hands-on work",
        "slower to build visual SOPs",
        "search isn’t tuned to step-by-step instructions"
      ]
    },
    {
      title: "why not obsidian?",
      points: [
        "great for power users, but high friction to adopt",
        "not purpose-built for capturing while you work",
        "harder to standardize across crews"
      ]
    }
  ];
</script>

<Nav />

<Hero { ...hero } centered />

<LogoScroller label="trusted by teams like yours" layout="horizontal" {logoUrls} />

<!-- How it works as features row -->
<section class="section-px section-py container mx-auto">
  <div class="mb-6">
    <h2 class="text-title1">how it works</h2>
    <p class="text-headline text-emphasis-low">three simple steps to capture, standardize, and share</p>
  </div>
  <div class="grid gap-6 md:grid-cols-3">
    {#each howItWorks as step}
      <article class="bg-card border-border rounded-(--radius) border p-6">
        <svelte:component this={step.icon} class="mb-3 h-6 w-6 opacity-70 text-primary" />
        <h3 class="text-title3 mb-1">{step.title}</h3>
        <p class="text-body text-emphasis-low">{step.description}</p>
      </article>
    {/each}
  </div>
</section>

<Features title="made for the factory floor" subtitle="everything you need to turn tribal knowledge into repeatable work" {features} />

<Stats {stats} class="bg-muted" />

<Testimonials {testimonials} />

<!-- Lightweight competitor comparison -->
<section class="section-px section-py container mx-auto">
  <h2 class="text-title1 mb-6">why squint instead</h2>
  <div class="grid gap-6 md:grid-cols-3">
    {#each comparison as block}
      <article class="bg-card border-border rounded-(--radius) border p-6">
        <h3 class="text-title3 mb-2">{block.title}</h3>
        <ul class="list-disc pl-5 text-body text-emphasis-low space-y-1">
          {#each block.points as p}
            <li>{p}</li>
          {/each}
        </ul>
      </article>
    {/each}
  </div>
</section>

<CallToAction
  title="standardize work without slowing it down"
  subtitle="capture in minutes, not months"
  description="see how teams like yours reduce ramp time and keep lines moving with visual, searchable instructions."
  imageSrc="https://images.unsplash.com/photo-1547825407-2d060104b6a5?w=600&h=750&fit=crop&auto=format"
  callsToAction={[{ href: "/demo", label: "Book a demo", variant: "primary" }, { href: "/overview", label: "Watch 60-sec overview", variant: "secondary" }]}
/>

<Footer />
