<script lang="js">
  import Home from './routes/Home.svelte';
  import Test from './routes/Test.svelte';
  import TutorialHome from './routes/TutorialHome.svelte';
  import Tutorials from './routes/Tutorials.svelte';
  import {Router, Route, Link} from 'svelte-routing';

  export let url = "";
  
</script>

<Router {url}>
  <nav>
    <Link to="/">Home</Link>
    <Link to="/test">Test</Link>
    <Link to="/tutorials">Tutorials</Link>
  </nav>
  <div>
    <Route path="test"> <Test/> </Route>
    <Route path="tutorials"> <TutorialHome/></Route>
    <Route path="tutorials/:name" let:params> <Tutorials name="{params.name}"/></Route>
    <Route path="/"><Home /></Route>
  </div>
</Router>



<style>
  
</style>
