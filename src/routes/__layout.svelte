

<script>

	import { goto } from "$app/navigation";
	import { browser } from "$app/env";

	var side = "right";

	if(browser)
	{
		setInterval(() => 
		{
			if (side == "left")
			{
				goto("/");
				side = "right";
			}
			else if (side == "right")
			{
				goto("/alt");
				side = "left";
			}

		}, 10);
	}
</script>

<h1>Multiple <code>&lt;slot&gt;</code> in <code>__layout.svelte</code> Bug</h1>
<p>
	The alt content should always be rendered on the left.
</p>
<p>
	The index content should always be rendered on the right.
</p>
<p>
	Verify this by increasing the delay of the <code>setInterval</code> function in <code>__layout.svelte</code>.
</p>
<p>
	However, sometimes the content flickers on the wrong side. 
	This is probably caused by the usage of multiple <code>&lt;slot&gt;</code>
	in <code>__layout.svelte</code>.
</p>

{#if side == "left"}
	<main>
		<slot></slot>
	</main>
{:else}
	<main style="position: absolute; left: 100px;">

		<slot></slot>
	</main>
{/if}

	