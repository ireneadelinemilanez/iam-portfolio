<script>
  import Kicker from '$lib/components/Article/Kicker.svelte';
  import Headline from '$lib/components/Article/Headline.svelte';
  import Image from '$lib/components/Media/Image.svelte';
  import Rule from '$lib/components/Layout/Rule.svelte';
  import TagList from '$lib/components/Data/TagList.svelte';
  import ArticleBody from '$lib/components/Article/ArticleBody.svelte';
  import { base } from '$app/paths';

  let { data } = $props();

  // Load Instagram embed script
  if (typeof window !== 'undefined') {
    const script = document.createElement('script');
    script.async = true;
    script.src = 'https://www.instagram.com/embed.js';
    document.body.appendChild(script);
  }
</script>

<div class="container">
  <Kicker text="{data.profile.name}'s Portfolio" href="{base}/" />
  <Headline text={data.clip.title} />

  <Image src={data.clip.image} alt={data.clip.title} />

  <Rule />

  <div class="content-grid" class:has-reel={data.clip.instagramReel}>
    <div class="left-column">
      <TagList label="Skills" tags={data.clip.skills} />
      <TagList
        label="View Project"
        tags={[{ text: new URL(data.clip.url).hostname, href: data.clip.url }]}
      />

      {#if data.clip.instagramReel}
        <ArticleBody>
          {#each data.clip.body.trim().split('\n\n') as paragraph, i (i)}
            <p>{paragraph}</p>
          {/each}
        </ArticleBody>
      {/if}
    </div>

    {#if data.clip.instagramReel}
      <div class="right-column">
        <div class="instagram-reel-container">
          <blockquote
            class="instagram-media"
            data-instgrm-permalink="{data.clip.instagramReel}"
            data-instgrm-version="14"
          >
          </blockquote>
        </div>
      </div>
    {/if}
  </div>

  {#if !data.clip.instagramReel}
    <Rule />
    <ArticleBody>
      {#each data.clip.body.trim().split('\n\n') as paragraph, i (i)}
        <p>{paragraph}</p>
      {/each}
    </ArticleBody>
  {/if}
</div>

<style lang="scss">
  @use '$lib/styles' as *;

  .content-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: var(--spacing-lg);
    align-items: start;

    &.has-reel {
      grid-template-columns: 1fr 1fr;

      @include mobile {
        grid-template-columns: 1fr;
      }
    }
  }

  .left-column {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
  }

  .instagram-reel-container {
    display: flex;
    justify-content: center;
    width: 100%;
  }
</style>