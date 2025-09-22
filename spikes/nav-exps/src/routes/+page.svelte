<script lang="ts">
  // Define the list of experiments
  const experiments = [
    { id: 'exp1', name: 'Experiment 1', path: '/exp1' },
    { id: 'exp2', name: 'Experiment 2', path: '/exp2' },
    { id: 'exp3', name: 'Experiment 3', path: '/exp3' }
  ];
</script>

<h1>Experiments</h1>

<ul>
  {#each experiments as exp}
    <li>
      <a href={exp.path}>{exp.name}</a>
    </li>
  {/each}
</ul>

<style>
  h1 {
    color: #333;
    margin-top: 3rem;
    margin-bottom: 1rem;
  }
  
  ul {
    list-style: none;
    padding: 0;
  }
  
  li {
    margin-bottom: 0.5rem;
  }
  
  a {
    color: #0066cc;
    text-decoration: none;
    padding: 0.5rem;
    display: block;
    border-radius: 4px;
    transition: background-color 0.2s;
  }
  
  a:hover {
    background-color: #f0f0f0;
  }
</style>