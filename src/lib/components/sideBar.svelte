<script>
	import { addRandomFish, coins, removeCoins, bait, addBait, removeBait } from '$lib/fishStore';

	let baitPrice = 10;

	function openModal() {
		const modal = document.getElementById('my_modal_2');
		if (modal instanceof HTMLDialogElement) modal.showModal();
	}

	function buyBait() {
		if ($coins >= baitPrice) {
			addBait(1);
			removeCoins(baitPrice);
		} else {
			alert('Not enough coins');
		}
	}

	function addFishAndRemoveBait() {
		if ($bait > 0) {
			addRandomFish();
			removeBait(1);
		} else {
			alert('Not enough bait');
		}
	}

	function buyAllBait() {
		const maxBait = Math.floor($coins / baitPrice);
		if (maxBait > 0) {
			addBait(maxBait);
			removeCoins(maxBait * baitPrice);
		} else {
			alert('Not enough coins');
		}
	}
</script>

<div class="flex gap-2">
	<p>Coins: {$coins.toFixed(2)}</p>
	<p>Bait: {$bait}</p>
</div>

<button
	class="btn border-primary hover:bg-primary hover:text-primary-content mb-2 border px-4 py-2"
	onclick={addFishAndRemoveBait}
	>Add Random Fish
</button>

<button class="btn" onclick={openModal}>Fishing Shop</button>
<dialog id="my_modal_2" class="modal">
	<div class="modal-box">
		<p class="pb-6">Coins: {$coins.toFixed(2)}</p>
		<button class="btn btn-primary mb-2" onclick={buyBait}>Bait x1 - ${baitPrice}</button>
		<button class="btn btn-primary" onclick={buyAllBait}>
			Buy All Bait ({Math.floor($coins / baitPrice)})
		</button>
	</div>
	<form method="dialog" class="modal-backdrop">
		<button>close</button>
	</form>
</dialog>
