<script lang="js">
  import Home from './routes/Home.svelte';
  import Test from './routes/Test.svelte';
  import TutorialHome from './routes/TutorialHome.svelte';
  import Tutorials from './routes/Tutorials.svelte';
  import {Router, Route, Link} from 'svelte-routing';
  import NavItem from './components/NavItem.svelte';
  import Academics from './routes/Academics.svelte';

  export let url = "";
  
</script>

<Router {url}>
  <nav>
    <NavItem name="Home" route="/"/>
    <NavItem name="Tutorials" route="/tutorials"/>
    <NavItem name="Academics" route="/academics"/>
  </nav>
  <div>
    <Route path="test"> <Test/> </Route>
    <Route path="tutorials"> <TutorialHome/></Route>
    <Route path="tutorials/:name" let:params> <Tutorials name="{params.name}"/></Route>
    <Route path="/"><Home /></Route>
    <Route path="academics"><Academics/></Route>
  </div>
</Router>



<style>
  :global(main) {
    margin-inline: 2rem;
    padding: 0;
  }
  :global(a) {
    text-decoration: none;
  }

  nav {
    justify-content: left;
  }
</style>
