# UiOverlay
The UiOverlay is an overlay component, best used as a base component for other components that should behave as an overlay. Eg Menus, Dialogs, Sheets

## Features ✨

 <ul>
  <li>Teleports to anywhere in the DOM</li>
  <li>Renders no wrapper element</li>
  <li>Traps focus within itself</li>
  <li>Keeps track of all active overlays</li>
 <li>Focuses on next active overlay when closed</li>
  <li>Supports transition</li>
 </ul>
 
## Props ⚙

| Name | Type | Default | Description |
| -----| ---- | ------- | ----------- |
| modelValue | ``Boolean`` | undefined | Used internally by ``v-model`` |
| disabled  | ``Boolean`` | undefined | This prop closes the ``<UiOverlay>`` if openedm and disallows any attempt to open | 
| to | ``String`` | 'body' | A valid ``querySelector`` to render the overlay. Throws an error if an invalid value is recieved |
| restoreScroll | ``Boolean`` | true | Use this if you want the previous ``window`` scroll positions to be restored when the ``<UiOverlay>`` is closed |
| restoreFocus | ``Boolean`` | true | Use this if you want to save the ``activeElement`` before the ``UiOverlay`` is opened, so the saved ``activeElement`` can be focused on when the ``UiOverlay`` is closed |

## Structure 🏗

````vue
<slot name='prepend'/>
    
 <props.tag data-ui-switch='' class='root'>
    <div class='track'>
      <slot name='track'/>
    </div>
      
    <div class='thumb'>
      <input/>
      <slot name='thumb' />
    </div>
 </props.tag> 
     
<slot name='append'/>   
````

## Slots 🎰 

<table>
 <thead>
  <tr>
    <th>Name</th><th>Payload</th><th>Description</th>
  </tr>
 </thead>
 <tbody>
  <tr>
    <td>prepend</td><td>
    <pre><code>{ 
  active: Boolean,
  validation: {
    message: '',
    valid: true
  },
  toggle: Function
}
</code></pre></td><td>Use this slot to render something else before the root component, commonly used for prepending a <code>&lt;label/&gt;</code></td>
  </tr>
   <tr>
     <td>track</td><td>Same as <em>prepend</em></td><td>Use this slot to render anything inside the <code>.track</code> element</td>
  </tr>
   <tr>
     <td>thumb</td><td>Same as <em>prepend</em></td><td>Use this slot to render anything inside the <code>.thumb</code> element</td>
  </tr>
   <tr>
     <td>default</td><td>Same as <em>prepend</em></td><td>Use this slot to render anything inside the root element</td>
  </tr>
   <tr>
     <td>append</td><td>Same as <em>prepend</em></td><td>Use this slot to render something else after the root component, commonly used for appending a <code>&lt;label/&gt;</code></td>
  </tr>
 </tbody>
</table>

<em>All slots are optional, and can accept multiple elements</em>

## Examples 💁‍♀️

 ### Simplest form
 
````vue
<div id='app'>
 <UiSwitch/>
</div>
````

### With v-model
 
````vue
<div id='app'>
 <UiSwitch v-model='switch'/>
</div>
````

### With an external ``<label>``
 
````vue
<div id='app'>
 <label for='switch'>
  Toggle UiSwitch
 </label>
 
 <UiSwitch id='switch' v-model='switch'/>
</div>
````

## With an internal ``<label>`` (prepend) and an internal validation message ``<span>`` (append)

````vue
<div id='app'>
 <UiSwitch id='switch'>
  <template v-slot:prepend='{active}'>
    <label for='switch'>
     Selected: {{active}}
    </label> 
  </template>
  
  <template v-slot:append='{validation, toggle}'>
    <span v-if='validation.message' @click='toggle'>
     Error!
    </span>
  </template>
 </UiSwitch>
</div>
````

## CSS variables 
<table>
 <thead>
  <tr>
    <th>Name</th><th>Default value</th><th>Description</th>
  </tr>
 </thead>
 <tbody>
  <tr>
    <td>--ui-height</td><td>28px</td><td>Use this variable to set the root element's height</td>
  </tr>
   <tr>
     <td>--ui-width</td><td>44px</td><td>Use this variable to set the root element's width</td>
  </tr>
   <tr>
     <td>--ui-track-height</td><td>100%</td><td>Sets the height of the track</td>
  </tr>
  <tr>
     <td>--ui-track-radius</td><td>100%</td><td>Sets the border-radius of the track</td>
  </tr>
 <tr>
     <td>--ui-track-background</td><td>#999</td><td>Sets the background of the track</td>
  </tr>
    <tr>
     <td>--ui-track-background-checked</td><td>#007bff</td><td>Sets the background of the track when the component is active</td>
  </tr>
    <tr>
      <td>--ui-thumb-size</td><td>25px</td><td>Sets the height and width of the <code>.thumb</code> element</td>
  </tr>
    <tr>
      <td>--ui-thumb-radius</td><td>50%</td><td>Sets the border-radius of the <code>.thumb</code> element</td>
  </tr>
    <tr>
      <td>--ui-thumb-offset</td><td>1.5px</td><td>The gap between the thumb and the edges</td>
  </tr>
    <tr>
      <td>--ui-thumb-translatex</td><td>
<pre><code>calc(var(--ui-width) - 
   var(--ui-thumb-size) - 
   var(--ui-thumb-offset)
)</code></pre></td><td>Computes the active state transformation</td>
  </tr>
  <tr>
      <td>--ui-thumb-background</td><td>#fff</td><td>The background of the thumb</td>
  </tr>
 </tbody>
</table>
