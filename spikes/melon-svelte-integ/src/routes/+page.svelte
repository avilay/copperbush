<script lang="ts">
  import TopNav from "./TopNav.svelte";

  const experiments = [
    { id: 'portal', name: 'Portal', path: '/portal' }
  ];
</script>

<TopNav />
<div class="container">
  <h1>Melon-Svelte Integration Experiments</h1>
  
  <ul>
    {#each experiments as exp}
      <li>
        <a href={exp.path}>{exp.name}</a>
      </li>
    {/each}
  </ul>
</div>

<style>
  .container {
    width: 90%;
    margin: 4em auto 0 2em;
    text-align: center;
  }
  
  ul {
    list-style: none;
    padding: 0;
  }
  
  li {
    margin-bottom: 0.5em;
  }
</style>