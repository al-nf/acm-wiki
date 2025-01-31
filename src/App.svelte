<script lang="js">
  import Home from './routes/Home.svelte';
  import Test from './routes/Test.svelte';
  import TutorialHome from './routes/TutorialHome.svelte';
  import Tutorials from './routes/Tutorials.svelte';
  import {Router, Route} from 'svelte-routing';
  import NavBar from './components/NavBar.svelte';
  import Academics from './routes/Academics.svelte';
  import CSENGlossary from './routes/CSENGlossary.svelte';

  export let url = "";
  
</script>

<Router {url}>
  <header>
    <h1>ACM Wiki</h1>
    <NavBar/>
  </header>
  
  <div class="container-fluid">
    <Route path="test"> <Test/> </Route>
    <Route path="tutorials"> <TutorialHome/></Route>
    <Route path="tutorials/:name" let:params> <Tutorials name="{params.name}"/></Route>
    <Route path="/"><Home /></Route>
    <Route path="academics"><Academics/></Route>
    <Route path="academics/csen-glossary"> <CSENGlossary/> </Route>
  </div>
</Router>



<style>
  :global(main) {
    margin-inline: 2rem;
    margin-top: 2rem;
    display: flex;
    flex-direction: column;
  }
  :global(a) {
    text-decoration: none;
  }
  header {
    background-color: #08347A;
    position: sticky;
    top: 0;
    flex-direction: row;
    align-items: flex-start;
    display: flex;
    height: 4rem;
  }
  h1 {
    margin-block: auto;
    margin-inline: 1rem;
  }</style>
