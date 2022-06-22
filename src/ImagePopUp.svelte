<script>
    export let image; 
    export let shown;
    const LEFT = -1;
    const RIGHT = 1;
    import {createEventDispatcher} from 'svelte';
    const dispatch = createEventDispatcher();
    
    // Transition shown to false when modal background or x is clicked. 
    const hide = () => 
    {
        dispatch('hide');
        console.log('here');
    }
    let scroll = 0;
    
    
    // Change photo left or right when user clicks buttons
    const moveSelected = (direction) => () => {
        dispatch('moveselected', direction);
    }   
    
    
    // Change photos for when user clicks left or right
    const keyUp = (event) => { 
        if(!shown)
            return;
        console.log('woot')
        switch(event.key){
            case "ArrowRight":
                moveSelected(RIGHT)();
            break;
            case "ArrowLeft":
                moveSelected(LEFT)();
            break;
            case "Escape":
                hide();
            break;
            default:
                console.log(event.key)
            break;
        }
    }
    // Remove scrolling capabilities when modal is open. 
    $:{
        if(shown){
            document.body.style.overflow = "hidden";
        }
        else
            document.body.style.overflow = "";
    }      
</script>
<svelte:window on:keyup={keyUp}/>
{#if shown && image !== null}
<section class="modal" on:click={hide}>
    <div class="left-button" on:click|stopPropagation = {moveSelected(LEFT)}>
        Click left
    </div>
    <div class="container" on:drag|stopPropagation>
            <img src={image.src} alt="somephoto" on:click|stopPropagation>
    </div>
    <div class="right-button" on:click|stopPropagation = {moveSelected(RIGHT)}>
        Click right
    </div>
</section>
{/if}

<style>
.modal{
    background-color: rgba(0,0,0,0.7);
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
}
img{
    width: 100%;
    height: 100%;
    object-fit: cover;
    position:absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0; 
    border-radius: 5px;
}
.container
{   
    position: relative;
    width: 50%; 
    padding-bottom: 50%;
    margin-left: auto;
    margin-right: auto;
}
.left-button, .right-button{
    cursor: pointer;
    background: grey;
    padding: 2rem;
}
</style>