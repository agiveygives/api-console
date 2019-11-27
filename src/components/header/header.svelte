<script>
  import TopAppBar, {Row, Section, Title, FixedAdjust, DenseFixedAdjust, ProminentFixedAdjust, ShortFixedAdjust} from '@smui/top-app-bar';
  import IconButton from '@smui/icon-button';

  let variant = 'fixed';
  let adjust = FixedAdjust

  switch (variant) {
    case 'fixed':
      variant = 'fixed';
      adjust = FixedAdjust;
    default:
      variant = 'fixed';
      adjust = FixedAdjust;
  }
</script>

<TopAppBar {variant} >
  <Row>
    <Section>
      <IconButton class="material-icons">menu</IconButton>
      <Title>API Console</Title>
    </Section>
    <Section align="end" toolbar>
      <IconButton class="material-icons" aria-label="Download">file_download</IconButton>
    </Section>
  </Row>
</TopAppBar>
<div use:FixedAdjust>
  <slot></slot>
</div>
