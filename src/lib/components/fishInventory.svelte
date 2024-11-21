<script lang="ts">
	import { inventory, totalWeight, removeFish, sellAllFish } from '$lib/fishStore';
</script>

<div class="text-primary-content p-4">
	<p>Total Weight: {$totalWeight.toFixed(2)} lbs</p>
	{#if $inventory.length === 0}
		<p>No fish in inventory</p>
	{/if}
	{#if $inventory.length > 0}
		<button
			class="btn border-primary hover:bg-primary hover:text-primary-content mb-2 border px-4 py-2"
			onclick={sellAllFish}>Sell All Fish</button
		>
		<p>Inventory:</p>
	{/if}
	<ul class="flex flex-wrap gap-2">
		{#each $inventory as fish, index}
			<li
				class="my-2 flex items-center justify-between divide-y divide-dashed rounded-xl border bg-gray-200 px-2 py-2 text-black"
			>
				<div>
					<div>{fish.name}</div>
					<div>Weight: {fish.minWeight.toFixed(2)} lbs</div>
				</div>
				<button
					class="btn btn-sm border-primary hover:bg-primary hover:text-primary-content ml-2"
					onclick={() => removeFish(index)}>🔙</button
				>
			</li>
		{/each}
	</ul>
</div>
