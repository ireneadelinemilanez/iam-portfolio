<script>
  import Profile from '$lib/components/Portfolio/Profile.svelte';
  import Card from '$lib/components/Data/Card.svelte';
  import CardGrid from '$lib/components/Data/CardGrid.svelte';
  import Rule from '$lib/components/Layout/Rule.svelte';
  import { base } from '$app/paths';

  let { data } = $props();
  const content = data.content;

  let profileSection = $state(null);

  const scrollToProfile = () => {
    profileSection?.scrollIntoView({ behavior: 'smooth' });
  };
</script>
  
<div class="container wide">
  <h1 onclick={scrollToProfile} role="button" tabindex="0">
  IRENE ADELINE MILANEZ
  </h1>

  <Rule />

  <h2> 
  ARTICLES 
  </h2>

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

  
  <div bind:this={profileSection}>
    <Profile
      name={content.profile.name}
      tagline={content.profile.tagline}
      photo={content.profile.photo}
      photoAlt={content.profile.photoAlt}
      email={content.profile.email}
      github={content.profile.github}
      linkedin={content.profile.linkedin}
      instagram={content.profile.instagram}
      bio={content.profile.bio}
    />
  </div>
</div>

<style lang="scss">
  h1 {
  transition: color 0.3s ease; /* Smoothly changes color over 0.3 seconds */
  }

  h1:hover {
  color: #638b22;
;
  }

</style>
