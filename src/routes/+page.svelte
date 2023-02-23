<script lang="ts">
    import Tasks from '../stores/Tasks.js';
    import Task from '../components/task.svelte';
    import Voice from '../components/voice.svelte';
    
    let inputVal = "";
    let tasks: any[] = [];
    let inputTxt: any;

    Tasks.subscribe(data => {
        tasks = data;
    });

    function handleSubmit(): void{
        if(!inputVal.trim()) return;

        Tasks.update((tasks: any[]) => {
            return [inputVal, ...tasks];
        });

        inputVal = "";
        inputTxt.focus();
    }
</script>

<main>
    <section id="leftSect">

    </section>
    <section id="rightSect">
        <form id="inpArea" on:submit|preventDefault={handleSubmit}>
            <!-- svelte-ignore a11y-autofocus -->
            <input 
                id="txtInp" 
                bind:this={inputTxt} 
                bind:value={inputVal} 
                autocomplete="off"
                autofocus 
                />
            <button id="addBtn" type="submit">Add</button>
        </form>
        <ul>
            {#each $Tasks as task, id}
                <li>
                    <Task 
                        task={task}
                        id={id}
                        />
                </li>
            {/each}
        </ul>
    </section>
</main>

<style>
    main{
        font-family: Arial, Helvetica, sans-serif;
        display: flex;
        height: 100%;
        width: 100%;
        }

    input{
        font-size: 1.5em;
        box-sizing: border-box; /* Include padding and border in element's total width */
        padding: 20px; /* Optional: Add some padding to the input element */
        }

    ul{
        margin: 0px;
        padding: 0px;
        }
        li{
            display: block;
            list-style:none;
            }

    #inpArea{
        display: flex;
        align-items: center;
        }
        #txtInp{
            flex: 8;
            padding: 5px;
            }
        #addBtn{
            flex: 1;
            padding: 5px;
            margin-left: 10px;
            }
        #leftSect{
            /* flex: 2; */
            min-width: 100px;
            position: relative;
            background-color:#F00;
            height: 100%;
            resize: both;
            display: block;
        }
        #rightSect{
            flex: 9;
            margin: 10px;
        }
</style>