<script>
  export let drawerItems = [];

  import Drawer, {AppContent, Content, Header, Title, Subtitle, Scrim} from '@smui/drawer';
  import List, {Item, Text, Separator, Subheader} from '@smui/list';
  import {stores} from '@sapper/app';

  const {page} = stores();

  function pickSection(section) {
    page.scrollTop = 0;

    // Svelte/Sapper is not updated the components correctly, so I need this.
    drawerItems.forEach(drawerItem => drawerItem.component.$set({activated: false}));
    section.component.$set({activated: true});
  }
</script>

<style>
  .drawer-container {
    flex-grow: 1;
    height: 100vh;
    display: flex;
  }
</style>

<div class="drawer-container">
  <Drawer>
    <Content>
      <List>
        {#each drawerItems as drawerItem}
          <Item
              bind:this={drawerItem.component}
              href={'route' in drawerItem ? drawerItem.route : drawerItem.shortcut}
              on:click={() => pickSection(drawerItem)}
              activated={'route' in drawerItem && drawerItem.route === $page.path}
              title={drawerItem.name}
              style="{drawerItem.indent ? 'margin-left: '+(drawerItem.indent * 25)+'px;' : ''}"
            >
              <Text class="mdc-theme--on-secondary">{drawerItem.name}</Text>
            </Item>
            {#if 'route' in drawerItem && $page.path.includes(drawerItem.route)
              && 'subsections' in drawerItem && drawerItem.subsections.length}
              <List>
                {#each drawerItem.subsections as subsection}
                  <Item
                    bind:this={subsection.component}
                    href={'route' in subsection ? subsection.route : subsection.shortcut}
                    on:click={() => pickSection(subsection)}
                    activated={'route' in subsection && subsection.route === $page.path}
                    title={subsection.name}
                    style="{subsection.indent ? 'margin-left: '+(subsection.indent * 25)+'px;' : ''}"
                  >
                    <Text class="mdc-theme--on-secondary">{subsection.name}</Text>
                  </Item>
                {/each}
              </List>
            {/if}
        {/each}
      </List>
    </Content>
  </Drawer>

  <AppContent class="app-content">
    <main class="main-content">
      <slot></slot>
    </main>
  </AppContent>
</div>