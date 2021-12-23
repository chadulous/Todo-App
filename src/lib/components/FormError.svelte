<script lang="ts">
	var messageelm: HTMLElement
	export function on(message) {
		messageelm.style.opacity = '1';
		messageelm.innerText = message;
	}
	export function off() {
		setTimeout(()=>{
			messageelm.style.opacity = '0';
			setTimeout(()=>{
				messageelm.innerText = ''
			}, 500)
		}, 500)
	}
</script>
<p bind:this={messageelm} class="text-red-500 text-xs errormes"></p>