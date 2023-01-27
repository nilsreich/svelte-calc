<script lang="ts">
	// This function will update the input variable with the symbol clicked on
	// The function is called by the onClick event of the buttons
	// The function is called with the event object as a parameter
	// The data-symbol attribute of the button is used to get the value of the symbol
	// The value of the symbol is then added to the input variable
	// The input variable is then used by the evaluate function to calculate the result

	let input = '';

	const update = async (e: any) => {
		removeRelease()
		input += e.target.dataset.symbol;
	};

	// When the user presses the backspace key, remove the last character in the input string.
	// If the user holds the backspace key down, keep removing characters at an interval.
	// The remove interval is set to 150 milliseconds.
	// The remove interval is cleared when the user releases the backspace key.
	let removeInterval:any;
	const remove = () => {
		input.length > 0 ? (input = input.slice(0, -1)) : null;
	};

	const removeHold = () => {
		removeInterval = setInterval(remove, 150);
	};

	const removeRelease = () => {
		clearInterval(removeInterval);
	};

	// This code solves an expression using the mathjs library.
	// It takes the expression from the input variable and
	// returns the result in the result variable.
	// The expression is evaluated with the evaluate function,
	// and the result is formatted with the format function.
	// The expression is replaced using the replaceAll function,
	// to replace any characters that are not allowed by mathjs.
	// The result is formatted to 14 decimal places using the
	// format function.
	let resultRounded='';

	const solve = async () => {
		// Import mathjs
		const { evaluate, format } = await import('mathjs');

		// Replace invalid characters
		let expression = input.replaceAll('−', '-');
		expression = expression.replaceAll(',', '.');
		expression = expression.replaceAll('×', '*');
		expression = expression.replaceAll('ℼ', 'pi');

		// Solve the expression and return the result
		let result = await evaluate(expression);
		resultRounded = await format(result, { precision: 14 }).toString();
	};

	const solveequation = async () => {
		// Import mathjs
		const { evaluate, format } = await import('mathjs');

		// Replace invalid characters
		let expression = input.replaceAll('−', '-');
		expression = expression.replaceAll(',', '.');
		expression = expression.replaceAll('×', '*');
		expression = expression.replaceAll('ℼ', 'pi');

		// Solve the expression and return the result
		let result = await evaluate(expression);
		resultRounded = await format(result, { precision: 14 }).toString();
	};
</script>



<div class="h-1/2 p-4 w-screen">
	<div
		class="text-6xl text-right overflow-scroll overflow-y-hidden scrollbar-hide whitespace-nowrap"
	>
		<span> &nbsp;</span>{input}
	</div>
	<div class="text-3xl text-right">
		{resultRounded}
	</div>
</div>
<div
	class="flex h-1/2 absolute bottom-0 w-full snap-x snap-mandatory overflow-scroll scrollbar-hide"
>
	<div class=" snap-start shrink-0 grid grid-cols-4 grow gap-2 py-4 w-screen ">
		<button on:click={update} data-symbol="(" class="btn btn-ghost text-2xl">(</button>
		<button on:click={update} data-symbol=")" class="btn btn-ghost text-2xl">)</button>
		<button on:click={update} data-symbol="^" class="btn btn-ghost text-2xl">^</button>
		<button
			on:click={remove}
			on:mousedown={removeHold}
			on:touchstart={removeHold}
			on:touchend={removeRelease}
			on:mouseup={removeRelease}
			class="btn btn-ghost text-2xl">⌫</button
		>
		<button on:click={update} data-symbol="7" class="btn btn-ghost text-2xl">7</button>
		<button on:click={update} data-symbol="8" class="btn btn-ghost text-2xl">8</button>
		<button on:click={update} data-symbol="9" class="btn btn-ghost text-2xl">9</button>
		<button on:click={update} data-symbol="+" class="btn btn-ghost text-2xl">+</button>
		<button on:click={update} data-symbol="4" class="btn btn-ghost text-2xl">4</button>
		<button on:click={update} data-symbol="5" class="btn btn-ghost text-2xl">5</button>
		<button on:click={update} data-symbol="6" class="btn btn-ghost text-2xl">6</button>
		<button on:click={update} data-symbol="−" class="btn btn-ghost text-2xl">−</button>
		<button on:click={update} data-symbol="1" class="btn btn-ghost text-2xl">1</button>
		<button on:click={update} data-symbol="2" class="btn btn-ghost text-2xl">2</button>
		<button on:click={update} data-symbol="3" class="btn btn-ghost text-2xl">3</button>
		<button on:click={update} data-symbol="×" class="btn btn-ghost text-2xl">×</button>
		<button on:click={update} data-symbol="," class="btn btn-ghost text-2xl">,</button>
		<button on:click={update} data-symbol="0" class="btn btn-ghost text-2xl">0</button>
		<button on:click={solve} class="btn btn-ghost text-2xl bg-opacity-0">=</button>
		<button on:click={update} data-symbol="/" class="btn btn-ghost text-2xl">/</button>
	</div>
	<div class="snap-start shrink-0  grid grid-cols-4 grow gap-2 py-4 w-screen ">
		<button on:click={update} data-symbol="ℼ" class="btn btn-ghost text-2xl">ℼ</button>
		<button on:click={update} data-symbol="e" class="btn btn-ghost text-2xl">e</button>
		<button on:click={update} data-symbol="=" class="btn btn-ghost text-2xl">=</button>
		<button on:click={solveequation} class="btn btn-ghost text-2xl">solve</button>

	</div>
</div>

<style>
	/* For Webkit-based browsers (Chrome, Safari and Opera) */
	.scrollbar-hide::-webkit-scrollbar {
		display: none;
	}

	/* For IE, Edge and Firefox */
	.scrollbar-hide {
		-ms-overflow-style: none; /* IE and Edge */
		scrollbar-width: none; /* Firefox */
	}
</style>
