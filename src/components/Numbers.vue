<template>
  <div>
    <div
      class="number"
      :id="'number-'+number"
      v-for="number in numArray()"
      :key="number"
      @mouseover="setDivisors(number)"
      @mouseout="reset">
      <!-- Attributes are easier to read in a column if there are many of them. -->
      {{number}}
    </div>
  </div>
</template>

<script>
export default {
  data()
  {
    return {
      numbers: []
    }
  },
  
  props: ['limit'], // The component shouldn't rely on ancestor state, so using props instead of watch to make this component more easily reusable.
  
  methods: {
    // changed name for two of the methods to be more self-explanatory.
    numArray() {
      let numbers = [];
      for(var i = 1; i <= this.limit; i++) // array needs to start from 1 as 0 can't be divided so doesn't make sense to render and last number should be the number entered into the input field.
      {
        numbers = [...numbers, i];
      }
      return numbers.sort(() => Math.random() - 0.5);
    },
    setDivisors(number) {
      const nums = document.querySelectorAll('.number');
      for(let i = 0; i < nums.length; i++)
      {
        const num = nums[i].textContent.trim();
        if(number % num === 0)
        {
          nums[i].classList.add('active')
          console.log('divisor', num)
        }
      }
    },
    reset() {
      const nums = document.querySelectorAll('.number');
      nums.forEach(num => num.classList.remove('active'))
    }
  }
}
</script>

<style scoped>
	.number {
		display: inline-block;
		padding: 5px;
		background-color: lightgrey;
		margin: 5px;
	}

	.active {
		background-color: red;
	}
</style>
