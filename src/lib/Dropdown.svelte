<svelte:options tag="twopine-dropdown" />

<script>
  let open = false;
  let divider = false;

</script>

<div class="dropdown">
  <div class:open={open} on:click="{() => open = !open}" class="button">
    Dropdown
  </div>

  <div class="menu">
    <slot class="item {divider}" name="item"/>
  </div>
</div>

<style>
  
a {
  text-decoration: none;
  color: var(--color-neutral);
}

a:hover {
  color: #222222
}

/* Dropdown */

.dropdown {
  display: inline-block;
  position: relative;
}

.button {
  display: inline-block;
  border: var(--border);
  border-radius: var(--border-radius);
  padding: 10px 30px 10px 20px;
  background-color: var(--color-primary-20);
  cursor: pointer;
  white-space: nowrap;
}

.button:after {
  transform: rotate(0deg); 
  transition: transform .2s ease-in-out;
  content: '';
  position: absolute;
  top: 50%;
  right: 15px;
  transform: translateY(-50%);
  width: 0; 
  height: 0; 
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 5px solid var(--color-neutral);
}

.button.open:after {
  transition: transform .2s ease-in-out;
  transform: rotate(180deg);
}

.button:hover {
  background-color: var(--color-primary-20);
}

.input {
  display: none;
}

.menu {
  position: absolute;
  top: 100%;
  border: 1px solid #ccc;
  border-radius: var(--border-radius);
  padding: 0;
  margin: 2px 0 0 0;
  box-shadow: var(--box-shadow);
  background-color: #ffffff;
  list-style-type: none;
}

.button ~ .menu {
  transition: all .2s ease-in-out;
  opacity: 0;
  height: 0;
  visibility: hidden;
  overflow: hidden;
} 

.button.open ~ .menu {
  transition: all .2s ease-in-out;
  opacity: 1;
  height: fit-content;
  visibility: visible;
} 

.menu .item {
  padding: 10px 20px;
  cursor: pointer;
  white-space: nowrap;
}

.menu .item::slotted(*) {
  display: block;
  margin: -10px -20px;
  padding: 10px 20px;
}

.menu .item::slotted(*:hover) {
  background-color: var(--color-primary-20);
}

.menu .item::slotted(.divider) {
  padding: 0;
  border-bottom: 1px solid var(--color-primary-20)
}
</style>