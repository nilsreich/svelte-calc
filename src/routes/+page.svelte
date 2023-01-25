<script lang="ts">

	let input = '';
	let result = '';

	const update = async (e: any) => {
		input += e.target.dataset.symbol;
	};

	const rem = () => {
		input.length > 0 ? (input = input.slice(0, -1)) : null;
	};

	const solve = async() => {
		var { evaluate, format } = await import('mathjs');
		
		// replace invalid characters
		let temp = input.replaceAll('−', '-');
		temp = temp.replaceAll(',', '.');
		temp = temp.replaceAll('×','*')

		let tempmath = await evaluate(temp);
		result = await format(tempmath, {precision: 14}).toString();
	};
</script>

<div class="flex h-screen flex-col">
	<div class="h-1/2 p-4">
		<div class="text-6xl text-right">
			{input}
		</div>
		<div class="text-3xl text-right">
			{result}
		</div>
	</div>
	<div class="grid grid-cols-4 grow gap-2 py-4">
		<button on:click={update} class="btn btn-ghost text-2xl">(</button>
		<button on:click={update} class="btn btn-ghost text-2xl">)</button>
		<button on:click={update} class="btn btn-ghost text-2xl">^</button>
		<button on:click={rem} class="btn btn-ghost ">rem</button>
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
		<button on:click={solve} class="btn btn-ghost text-2xl">=</button>
		<button on:click={update} data-symbol="/" class="btn btn-ghost text-2xl">/</button>
	</div>
</div>
