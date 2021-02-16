<template>
	<main class="">
	
	
	</main>
</template>

<script>
// import DreamyInput from './components/DreamyInput.vue'


export default {
	name: 'aCoolAppByTiffachoo',
	components: {
		
		// DreamyInput
	},
	data() {
		return {
			emailValue: '',
			emailIsDisabled: false,
			emailText: '',
			isValid: false,
			isNotValid: false
		}
	},
	methods: {
		submitMail() {
			alert(this.emailValue)
		},
		animateText() {
			const tlJiggle = gsap.timeline({ 
				delay: 1, 
				defaults: {
					duration: 0.1
				}
			});
			
			tlJiggle
				.to('.input-text-letter', {
					y: 'random(-6, 4)'
				})
				.to('.input-text-letter', {
					y: 'random(-6, 4)'
				})
				.to('.input-text-letter', {
					y: 'random(-6, 4)'
				})
				.to('.input-text-letter', {
					y: 'random(-6, 4)'
				})
				.to('.input-text-letter', {
					y: 0,
					duration: 0.1
				})
				.to('.input-text-letter', {
					delay: 0,
					duration: 0.5,
					ease: 'expo.in',
					x: 300,
					stagger: {
						amount: 0.3,
						from: 'end'
					}
				});
		},
		reset() {
			this.emailIsDisabled = false;
			this.isValid = false;
			this.isNotValid = false;
			this.emailText = '';
		}
	}
}
</script>

<style >
:root {
  --black: #87213c;
  --white: #fff;
  --primary-color: #f9dde3;
  --primary-color-tint: #fcf2f5;
  --secondary-color: #ff2961;
  --accent-color: #fae798;
  --mail-color: #326dcc;
  --star-color: #fae798;
  --star-sparkly-color: #b8d7ff;
}

* {
  box-sizing: border-box;
}

body {
  display: grid;
  place-items: center;
  min-height: 100vh;
  background-color: var(--primary-color-tint);
  font-size: 16px;
  line-height: 1;
  font-family: "Fredoka One", sans-serif;
}

.container {
  display: grid;
  grid-template-columns: 2fr 1fr;
  align-items: center;
  width: 100%;
  max-width: 400px;
}

.input-text {
  position: absolute;
  z-index: 5;
  width: 17rem;
  font-size: 1.25rem;
  line-height: 1.5;
  color: var(--black);
  transform: translate(1rem, 0.625rem);
  overflow: hidden;
}
.input-text-letter {
  display: inline-block;
  transform-origin: center bottom;
}

.input-wrap {
  position: relative;
}

.cloudy {
  position: absolute;
  top: 50%;
  left: 50%;
      width: 280%;
    z-index: -1;
  transform: translate(-50%, -50%);
}
.cloudy-poofs {
  fill: var(--white);
}

.fade-enter-active, .fade-leave-active {
  transition: 0.3s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

.dreamy-input {
    margin: 40px auto;
  --offset-top: 0.1875rem;
  --offset-left: -0.125rem;
  --control-height: 3.125rem;
  position: relative;
}
.dreamy-input::after {
  content: "";
  position: absolute;
  top: var(--offset-top);
  left: var(--offset-left);
  height: 100%;
  width: 100%;
  border: 3px solid var(--black);
  pointer-events: none;
  transition: border 0.5s ease-in-out;
}
.dreamy-input::after, .dreamy-input-control {
  border-radius: var(--control-height);
}
.dreamy-input-control {
  width: 15.625rem;
  height: var(--control-height);
  padding: 0 calc(1rem + var(--control-height)) 0 1rem;
  border: 0;
  background-color: var(--primary-color);
  font-family: "Fredoka One", sans-serif;
  font-size: 1.25rem;
  color: var(--black);
  caret-color: var(--secondary-color);
  transition: background-color 0.5s ease-in-out;
}
.dreamy-input-control:focus {
  outline: none;
}
.dreamy-input-control:disabled {
  background-color: var(--primary-color-tint);
}
.dreamy-input:focus-within::after {
  border-color: var(--secondary-color);
}
.dreamy-input-label, .dreamy-input-error {
  position: absolute;
  left: 1rem;
  font-size: 0.75rem;
  letter-spacing: 0.05em;
}
.dreamy-input-label {
  top: -0.75rem;
  color: var(--black);
}
.dreamy-input-error {
  bottom: -1.5rem;
  color: var(--secondary-color);
}
.dreamy-input-button {
  display: grid;
  place-items: center;
  position: absolute;
  top: calc(var(--offset-top) + 3px);
  right: 0;
  height: var(--control-height);
  width: var(--control-height);
  padding: 0;
  border: 0;
  background-color: transparent;
  color: var(--white);
  cursor: pointer;
  transition: 0.4s ease-in-out;
}
.dreamy-input-button-star {
  fill: currentColor;
  stroke: var(--star-stroke, transparent);
  stroke-width: 3px;
}
.dreamy-input-button-svg {
  width: 40%;
  overflow: visible;
}
.dreamy-input-button:focus {
  outline: none;
  color: var(--secondary-color);
}
.dreamy-input-button:hover {
  --star-stroke: var(--black);
  transform: scale(1.2);
  color: var(--accent-color);
}
.dreamy-input.disabled::after {
  border-color: var(--primary-color);
}
.dreamy-input.disabled .dreamy-input-button {
  color: var(--primary-color);
}
</style>
