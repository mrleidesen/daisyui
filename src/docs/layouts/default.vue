<template>
<div>
  <Header/>
  <div class="drawer drawer-mobile">
    <input id="main-menu" type="checkbox" class="drawer-toggle" v-model="showMainMenu" >
    <main class="flex-grow block pt-16 overflow-x-hidden bg-base-100 text-base-content drawer-content">
      <div class="p-4 lg:p-10">
        <Nuxt />
      </div>

    </main>
    <div class="drawer-side">
      <label for="main-menu" class="drawer-overlay"></label>
      <aside class="flex flex-col justify-between pt-16 border-r border-base-200 bg-base-100 text-base-content w-80">
        <div>
          <Menu class="flex flex-col p-4 pt-2 compact">
            <MenuItem class="mt-4 menu-title">
              <span>
                Docs
              </span>
            </MenuItem>
            <MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/docs/install">
                <Icon glyph="inbox-in" class="inline-block w-6 h-6 mr-2 stroke-current" />
                install
              </NuxtLink>
            </MenuItem>
            <MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/docs/use">
                <Icon glyph="lightning-bolt" class="inline-block w-6 h-6 mr-2 stroke-current" />
                use
              </NuxtLink>
            </MenuItem>
            <MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/docs/customize">
                <Icon glyph="code" class="inline-block w-6 h-6 mr-2 stroke-current" />
                customize components
              </NuxtLink>
            </MenuItem>
            <MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/docs/default-themes">
                <Icon glyph="color-swatch" class="inline-block w-6 h-6 mr-2 stroke-current" />
                Themes
              </NuxtLink>
            </MenuItem>
            <MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/docs/config">
                <Icon glyph="adjustments" class="inline-block w-6 h-6 mr-2 stroke-current" />
                config
              </NuxtLink>
            </MenuItem>
            <!--<MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/docs/features">
                <Icon glyph="check" class="inline-block w-6 h-6 mr-2 stroke-current" />
                Features
              </NuxtLink>
            </MenuItem>
            <MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/docs/whats-included">
                <Icon glyph="info" class="inline-block w-6 h-6 mr-2 stroke-current" />
                What's included?
              </NuxtLink>
            </MenuItem>-->
          <!--</Menu>
          <Menu class="flex flex-col p-4 pt-0 compact">
            <MenuItem class="menu-title">
              <span>
                Core
              </span>
            </MenuItem>-->
            <MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/core/colors">
                <Icon glyph="color" class="inline-block w-6 h-6 mr-2 fill-current" />
                Colors
              </NuxtLink>
            </MenuItem>
            <MenuItem>
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" to="/core/layout">
                <Icon glyph="text" class="inline-block w-6 h-6 mr-2 fill-current" />
                Layout & Typography
              </NuxtLink>
            </MenuItem>
          </Menu>
          <Menu class="flex flex-col p-4 pt-0 compact">
            <MenuItem class="menu-title">
              <span>
                Components
              </span>
            </MenuItem>
            <MenuItem v-for="(item, itemindex) in componentPages" v-bind:key="item.itemindex" v-bind:class="{ 'disabled' : !item.path }">
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize justify-between" v-if="item.path" :to="item.path">
                {{ item.name }}
                <span v-if="item.new" class="badge badge-sm">new</span>
                <span v-if="item.updated" class="badge badge-sm badge-outline">updated</span>
              </NuxtLink>
            </MenuItem>
            <MenuItem class="mt-4 menu-title">
              <span>
                Demos
              </span>
            </MenuItem>
            <MenuItem v-for="(item, itemindex) in demoPages" v-bind:key="item.itemindex" v-bind:class="{ 'disabled' : !item.path }">
              <NuxtLink v-on:click.native="showMainMenu = false" class="capitalize" v-if="item.path" :to="item.path">
                {{ item.name }}
              </NuxtLink>
            </MenuItem>
          </Menu>
        </div>
      </aside>
    </div>
  </div>
  </div>
</template>

<script>
import {themeChange} from "theme-change"
export default {
  props: {
    classes: String
  },
  data() {
    return {
      docPages: [],
      corePages: [],
      componentPages: [],
      demoPages: [],
      showMainMenu: false,
      newComponents: [
        'collapse',
        'carousel',
        'dropdown',
        'tooltip',
        'stat',
        'steps',
        'table',
      ],
      updatedComponents: [
        'avatar',
      ],
    }
  },
  created () {
    this.$router.options.routes.forEach((routeOption) => {
      if (routeOption.path.startsWith('/docs')) {
        this.docPages.push({
          name: routeOption.name.replace("docs-", ""),
          path: routeOption.path,
        })
      }
    })
    this.$router.options.routes.forEach((routeOption) => {
      if (routeOption.path.startsWith('/core')) {
        this.corePages.push({
          name: routeOption.name.replace("core-", ""),
          path: routeOption.path,
        })
      }
    })
    this.$router.options.routes.forEach((routeOption) => {
      if (routeOption.path.startsWith('/components')) {
        this.componentPages.push({
          name: routeOption.name.replace("components-", ""),
          path: routeOption.path,
          new: this.newComponents.includes(routeOption.name.replace("components-", "")),
          updated: this.updatedComponents.includes(routeOption.name.replace("components-", "")),
        })
      }
    })
    this.$router.options.routes.forEach((routeOption) => {
      if (routeOption.path.startsWith('/demos')) {
        this.demoPages.push({
          name: routeOption.name.replace("demos-", ""),
          path: routeOption.path,
        })
      }
    })
  },
  mounted(){
    themeChange(false)
  },
}
</script>
