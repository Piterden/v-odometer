<template>
	<span :class="className"></span>
</template>

<script>
	export default {
		name: "VueOdometer",
		props: {
			className:{
				type: String,
				default: "odometer"
			},
			value: {
				type: Number,
				required: false,
				default: 0
			},
			format: {
				type: String,
				required: false,
				default: '(.ddd),dd'
			},
			theme: {
				type: String,
				required: false,
				default: 'minimal'
			},
			duration: {
				type: Number,
				required: false,
				default: 3000
			},
			animation: {
				type: String,
				required: false,
				default: 'count'
			},
			formatFunction: {
				type: Function,
				required: false
			}
		},
		data: function () {
			return {
				instance: null
			}
		},
	    watch: {
	      value: {
	        handler: function(value)
	        {
	          if (this.instance && this.instance.update) {
	            this.instance.update(value);
	          }
	        },
	        deep: false
	      }
	    },
	    mounted: function () {
	    	this.instance = new Odometer({
	    		el: this.$el,
	    		value: this.value,
	    		theme: this.theme,
	    		format: this.format,
	    		duration: this.duration,
	    		animation: this.animation
	    	})

	    	this.instance.render()
	    }
	}
</script>