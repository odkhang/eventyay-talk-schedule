<template>
  <div v-on-clickaway="away" class="app-drop-down">
    <bunt-button @click="toggle">
      <slot name="toggler"> Toggle </slot>
      <svg
        v-if="this.sharedState.active"
        xmlns="http://www.w3.org/2000/svg"
        width="1em"
        height="1em"
        viewBox="0 0 24 24"
      >
        <path fill="currentColor" d="m7 15l5-5l5 5z" />
      </svg>
      <svg
        v-else
        xmlns="http://www.w3.org/2000/svg"
        width="1em"
        height="1em"
        viewBox="0 0 24 24"
      >
        <path fill="currentColor" d="m7 10l5 5l5-5z" />
      </svg>
    </bunt-button>
    <slot />
  </div>
</template>
<script>
import { mixin as clickaway } from 'vue-clickaway'

export default {
	name: 'AppDropdown',
	mixins: [clickaway],
	provide () {
		return {
			sharedState: this.sharedState
		}
	},
	data () {
		return {
			sharedState: {
				active: false,
			},
		}
	},
	methods: {
		toggle () {
			this.sharedState.active = !this.sharedState.active
		},
		away () {
			this.sharedState.active = false
		}
	}
}
</script>
<style>
.app-drop-down {
  margin: 0px 4px;
  border-radius: 5px;
  border: 2px solid rgba(0, 0, 0, 0.38);
}

.app-drop-down .bunt-button {
  background-color: white;
}

.app-drop-down .bunt-button .bunt-button-content {
  text-transform: capitalize;
}
</style>
