<template>
    <div class="quantity-selector">
        <div class="btn-group btn-group-sm" role="group">
            <button v-for="quantity in range"
                    @click="select(quantity)"
                    type="button"
                    :class="{ 'btn btn-outline-secondary': true, 'active': quantity === value }"
            >
                {{ quantity }}
            </button>
        </div>
    </div>
</template>

<script>
  import range from 'lodash/range';

  export default {
    name: 'builder-quantity-selector',
    props: {
      min: {
        type: Number,
        default: () => 0,
      },
      max: {
        type: Number,
        required: true,
      },
      current: {
        type: Number,
        required: true,
      },
    },
    watch: {
      current() {
        this.value = this.current;
      },
    },
    data() {
      return {
        value: this.current,
      };
    },
    computed: {
      range() {
        return range(this.min, this.max + 1);
      },
    },
    methods: {
      select(value) {
        this.value = value;
        this.$emit('change', value);
      },
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
