<template>
  <nuxt-link
    v-if="!childComponents.length && hasPermittedRole"
    class="navbar-item"
    :to="toRoute"
    :active-class="activeClass"
    :exact="toRoute === '/'"
  >
    <span :class="component.className">{{ component.label }}</span>
  </nuxt-link>
  <div
    v-else-if="hasPermittedRole"
    class="navbar-item has-dropdown is-hoverable"
  >
    <nuxt-link
      class="navbar-link"
      :to="toRoute"
      :active-class="activeClass"
      :exact="toRoute === '/'"
    >
      <span :class="component.className">{{ component.label }}</span>
    </nuxt-link>
    <div
      v-for="(group, groupIndex) in childComponents"
      :key="'nbigroup-' + groupIndex"
      class="navbar-dropdown"
    >
      <bulma-navbar-item
        v-for="(childComponent, index) in group"
        :key="'nbicc-' + index"
        :component="childComponent"
      />
    </div>
  </div>
</template>

<script>
import NavItemMixin from '../navItemMixin'

export default {
  name: 'BulmaNavbarItem',
  mixins: [NavItemMixin],
  computed: {
    navbarItemClass() {
      return this.component.className || 'navbar-item'
    }
  }
}
</script>
