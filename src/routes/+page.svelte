<script>
  import Profile from '$lib/components/Portfolio/Profile.svelte';
  import Card from '$lib/components/Data/Card.svelte';
  import CardGrid from '$lib/components/Data/CardGrid.svelte';
  import { base } from '$app/paths';

  let { data } = $props();
  const content = data.content;
</script>

<div class="container wide">
  <Profile
    name={content.profile.name}
    tagline={content.profile.tagline}
    photo={content.profile.photo}
    photoAlt={content.profile.photoAlt}
    email={content.profile.email}
    github={content.profile.github}
    linkedin={content.profile.linkedin}
    bio={content.profile.bio}
  />

  <h1>
  Articles
  </h1>

   <CardGrid>
    {#each content.clips as clip (clip.title)}
      <Card
        href="{base}/clips/{clip.slug}"
        image={clip.image}
        imageAlt={clip.title}
      >
        <h3>{clip.title}</h3>
        <p>{clip.description}</p>
      </Card>
    {/each}
  </CardGrid>
</div>
