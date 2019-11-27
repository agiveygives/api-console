<script>
  import Header from '../components/header/header';
  import SideDrawer from '../components/sideDrawer/sideDrawer.svelte';
  import { navConfig } from './nav-confg.js';
</script>

<style>
  :global(.main-content) {
    position: relative;
    max-width: 56em;
    background-color: white;
    padding: 2em;
    margin: 0 auto;
    box-sizing: border-box;
  }
</style>


<Header>
  <SideDrawer drawerItems={navConfig}>
    <slot></slot>
  </SideDrawer>
</Header>