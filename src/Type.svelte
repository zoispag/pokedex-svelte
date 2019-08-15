<script>
  export let type;

  $: typeClass = `ml-1 type-${type.name}`;

  function capitalize(val) {
    if (!val) return ''
    val = val.toString()
    return val.charAt(0).toUpperCase() + val.slice(1)
  }
</script>

<div class={typeClass}>
    <span>{ capitalize(type.name) }</span>
</div>
