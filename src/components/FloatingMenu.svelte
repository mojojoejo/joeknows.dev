<script lang="ts" context="module">
import { writableSet } from "../stores";
export interface FloatingMenuContext {
	active: any;
	items: ReturnType<typeof writableSet>;
	activate: (id: any) => void;
	deactivate: (id: any) => void;
}

export const FLOATING_MENU_KEY = {};
</script>

<script lang="ts">
import { setContext } from "svelte";
import { writable } from "svelte/store";

const items = writableSet<any>();

let active: any = writable<any>(null);

setContext<FloatingMenuContext>(FLOATING_MENU_KEY, {
	active,
	items,
	activate,
	deactivate,
});

function activate(id: any) {
	$active = id;
}

function deactivate(id: any) {
	if ($active === id) {
		$active = null;
	}
}
</script>

<div class="fixed z-20 right-3 top-3">
	<slot />
</div>
