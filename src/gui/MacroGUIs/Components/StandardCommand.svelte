<script lang="ts">
    import {ICommand} from "../../../types/macros/ICommand";
    import {faTrash, faBars} from "@fortawesome/free-solid-svg-icons";
    import Icon from "svelte-awesome/components/Icon.svelte";
    import {createEventDispatcher} from "svelte";
    import {DndEvent} from "svelte-dnd-action";

    export let command: ICommand;
    export let startDrag: (e: CustomEvent<DndEvent>) => void;
    export let dragDisabled: boolean;
    const dispatch = createEventDispatcher();

    function deleteCommand(commandId: string) {
        dispatch('deleteCommand', commandId);
    }
</script>

<div class="quickAddCommandListItem">
    <li>{command.name}</li>
    <div>
        <span on:click={() => deleteCommand(command.id)} class="clickable">
            <Icon data="{faTrash}" />
        </span>
        <span on:mousedown={startDrag} on:touchstart={startDrag}
              aria-label="Drag-handle"
              style="{dragDisabled ? 'cursor: grab' : 'cursor: grabbing'};"
              tabindex={dragDisabled ? 0 : -1}
        >
            <Icon data={faBars} />
        </span>
    </div>
</div>

<style lang="css">

</style>