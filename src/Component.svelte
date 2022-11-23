<script>
  import "@spectrum-css/progressbar/"
  import { getContext } from "svelte"

  export let label = "Progress"
  export let labelPosition
  export let value
  export let fillColor
  export let size 
  export let indeterminate
  
  // Internal 
  let thickness 
  $: switch (size) {
      case 'S':
        thickness = "0.25rem"
        console.log(fillColor)
        break;
      case 'M':
        thickness = "0.45rem"
        break;
      case 'L':
        thickness = "0.65rem"
        break;
      case "XL":
        thickness = "0.85rem"
        break;
    }

  const { styleable } = getContext("sdk")
  const component = getContext("component")
</script>

<div use:styleable={$component.styles}>
  <div 
    class="spectrum-ProgressBar spectrum-ProgressBar--size{size}" 
    class:spectrum-ProgressBar--sideLabel = {labelPosition === "left"}
    class:spectrum-ProgressBar--indeterminate = {indeterminate}
    value="{value}" 
    role="progressbar" 
    aria-valuenow="{value}" 
    aria-valuemin="0" 
    aria-valuemax="100"
    style="--spectrum-progressbar-fill-color: {fillColor ? fillColor : "var(--primaryColor)"}; 
           --spectrum-progressbar-track-color: var(--spectrum-global-color-gray-300);
           --spectrum-progressbar-thickness: {thickness};
           width: 100%;
           "
    >
      <div class="spectrum-FieldLabel spectrum-FieldLabel--size{size} spectrum-ProgressBar-label">{label}</div>
      <div class="spectrum-FieldLabel spectrum-FieldLabel--size{size} spectrum-ProgressBar-percentage">{value}%</div>
      <div class="spectrum-ProgressBar-track">
        <div class="spectrum-ProgressBar-fill" style="width: {value}%;"></div>
      </div>
  </div>  
</div>