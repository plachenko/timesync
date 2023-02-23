<script lang="ts">
  import { onMount } from 'svelte';
    import Tasks from '../stores/Tasks.js';

    export let task: any;
    export let id: number;

    let done = false;
    let taskObj;

    onMount(() => {
        taskObj = {
            id: id,
            task: task,
            done: false
        }

    });


    function finishTask(): any{
        console.log(idx);
    }

    function removeItem(){
        console.log(Tasks);
    }

    function clickEvt(e: PointerEvent): any{
        // console.log('clicked.', e.target);
        // let el: any = e.target;
        console.log('donning the task.');
        taskObj.done = !taskObj.done;
    }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="task {taskObj.done ? 'done' : ''}" on:click={() => clickEvt}>
    <span>{taskObj.task}</span>
</div>

<style>
.task{
    background-color: rgba(0, 255, 0, .2);
    font-size: 1.5em;
    padding: 15px 20px;
    border-radius: 10px;
    margin: 5px 0px;
    cursor: pointer;
    user-select: none;
    }
    .task button{
        float: right;
        }
    .done{
        background-color: #EEE;
        color: #CCC;
        text-decoration: line-through;
        }
</style>
