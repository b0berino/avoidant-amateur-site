<script>
    import ImagePopUp from "./ImagePopUp.svelte";
    let selected = null;
    let shown = false;
    let images = [
    {src:"build/images/CorinneSample1.jpeg", index: 4},
    {src:"build/images/CorinneSample2.jpeg", index: 5},
    {src: 'build/images/CorinneSample3.jpeg', index: 6}
]
    const setImage = (image) => () => {
        selected = image;
        shown = true;
    }
    const hide = () => {
        shown = false;
    }
    
    const handleMove = (event) => 
    {
        const direction = event.detail;
        if(images[selected.index + direction]){
            selected = images[selected.index + direction];
        }
        };

</script>
<div class="center">
<div class="grid">
{#each images as image}
    <div class="block" on:click={setImage(image)} >
        <img src={image.src} alt="it's a doggy">
    </div>
    <ImagePopUp shown={shown} image={selected} on:hide = {hide} on:moveselected = {handleMove}/>
{/each}
</div>
</div>
<style>

.grid
{
    display: grid;
    gap: 0.1rem;
    width: 100%;
    padding-left: 1rem;
    padding-right: 1rem;
}
.center{
    display: flex;
    align-items: center;
    width: 100%;
    justify-content: center;
    padding-top: 1rem;
    padding-bottom: 1rem;
}
 @supports (width: min(80ch, 100%)) {
.grid
{
    grid-template-columns: repeat(auto-fit, minmax(min(20ch, 100%), 1fr));
    gap: 0.5rem;
    row-gap: 1rem;
    max-width: var(--max);
}

}

.block{
    background: grey;
    border-radius: 5px;
    padding-bottom: 100%; 
    cursor: pointer;
    position:relative;
    transition: opacity 0.3s;
}
.block > *
{
    overflow: hidden;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
}
img{
    width: 100%;
    height: 100%;
    display: block;
    object-fit: cover;
    border-radius: 5px;
}
.block:hover{
    opacity: 50%;
}

</style>