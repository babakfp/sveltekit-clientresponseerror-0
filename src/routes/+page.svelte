<script>
	import { onMount } from "svelte"
	import PocketBase from "pocketbase"
	import { PUBLIC_POCKETBASE_URL } from "$env/static/public"
	import { messages } from "$lib/messages.js"

	const pb = new PocketBase(PUBLIC_POCKETBASE_URL)

	let errorObject
	let actionName

	onMount(async () => {
		try {
			await pb
				.collection("messages")
				.subscribe("*", async ({ action, record }) => {
					actionName = action
				})
		} catch (error) {
			errorObject = error
		}
	})
</script>

<div>{PUBLIC_POCKETBASE_URL}</div>
<br />
<div>
	errorObject:<br />{JSON.stringify(errorObject)}
</div>
<br />
<div>
	actionName:<br />{JSON.stringify(actionName)}
</div>
