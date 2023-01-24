<script lang="ts">
	import { evaluate } from 'mathjs';
	let input = '';
	let result = '';

	const update = (e: any) => {
		input += e.target.dataset.symbol;
	};

	const rem = () => {
		input.length > 0 ? (input = input.slice(0, -1)) : null;
	};

	const solve = () => {
		result = evaluate(input).toString();
	};
</script>

<div class="flex h-screen flex-col">
	<div class="h-1/2">
		<div class="text-6xl text-right">
			{input}
		</div>
		<div class="text-3xl text-right">
			{result}
		</div>
	</div>
	<div class="grid grid-cols-4 grow text-xl gap-2 py-4">
		<button on:click={update} data-symbol="(" class="btn btn-ghost ">(</button>
		<button on:click={update} data-symbol=")" class="btn btn-ghost ">)</button>
		<button on:click={update} data-symbol="^" class="btn btn-ghost ">^</button>
		<button on:click={rem} class="btn btn-ghost ">rem</button>
		<button on:click={update} data-symbol="7" class="btn btn-ghost ">7</button>
		<button on:click={update} data-symbol="8" class="btn btn-ghost">8</button>
		<button on:click={update} data-symbol="9" class="btn btn-ghost">9</button>
		<button on:click={update} data-symbol="+" class="btn btn-ghost">+</button>
		<button on:click={update} data-symbol="4" class="btn btn-ghost">4</button>
		<button on:click={update} data-symbol="5" class="btn btn-ghost">5</button>
		<button on:click={update} data-symbol="6" class="btn btn-ghost">6</button>
		<button on:click={update} data-symbol="-" class="btn btn-ghost">-</button>
		<button on:click={update} data-symbol="1" class="btn btn-ghost">1</button>
		<button on:click={update} data-symbol="2" class="btn btn-ghost">2</button>
		<button on:click={update} data-symbol="3" class="btn btn-ghost">3</button>
		<button on:click={update} data-symbol="*" class="btn btn-ghost">*</button>
		<button on:click={update} data-symbol="." class="btn btn-ghost">,</button>
		<button on:click={update} data-symbol="0" class="btn btn-ghost">0</button>
		<button on:click={solve} class="btn btn-ghost">=</button>
		<button on:click={update} data-symbol="/" class="btn btn-ghost">/</button>
	</div>
</div>
