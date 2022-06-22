<script>
import Grid from './Grid.svelte'
import Walkway from 'walkway.js';
import { onMount } from 'svelte';
const scrollTo = (id) => () => document.getElementById(id).scrollIntoView({behavior: 'smooth'});
let scrollable = false;
let selected = 1;
let tabs = [
    {id: 1, label: 'Main', action: scrollTo("slide-1")}, 
    {id: 2, label: 'Archive', action: scrollTo("bottom-archive")}, 
    {id: 3, label: 'About', action: scrollTo("slide-2")}
];
const meme = `What the fuck did you just fucking say about me, you little bitch? I’ll have you know I graduated top of my class in the Navy Seals, and I’ve been involved in numerous secret raids on Al-Quaeda, and I have over 300 confirmed kills. I am trained in gorilla warfare and I’m the top sniper in the entire US armed forces. You are nothing to me but just another target. I will wipe you the fuck out with precision the likes of which has never been seen before on this Earth, mark my fucking words. You think you can get away with saying that shit to me over the Internet? Think again, fucker. As we speak I am contacting my secret network of spies across the USA and your IP is being traced right now so you better prepare for the storm, maggot. The storm that wipes out the pathetic little thing you call your life. You’re fucking dead, kid. I can be anywhere, anytime, and I can kill you in over seven hundred ways, and that’s just with my bare hands. Not only am I extensively trained in unarmed combat, but I have access to the entire arsenal of the United States Marine Corps and I will use it to its full extent to wipe your miserable ass off the face of the continent, you little shit. If only you could have known what unholy retribution your little “clever” comment was about to bring down upon you, maybe you would have held your fucking tongue. But you couldn’t, you didn’t, and now you’re paying the price, you goddamn idiot. I will shit fury all over you and you will drown in it. You’re fucking dead, kiddo.`;
const svg = new Walkway({selector: "#lollipop", duration: '2300', easing: function(t){return t*t}});
</script>
<header>
		<!-- CAROUSEL  -->
	<section class="carousel">
		<div class="slides">
        	<div class="slide" id="slide-1">	
				<section class="main-page">
					<img id="lollipop" src="/build/images/CorinneMain.svg"  alt="lollipop" on:click={svg.draw}>
					<h1> Avoidant Amateur</h1>
					<h2> Ink & Digital Art</h2>	
				</section>
			</div>
        	<div class="slide" id="slide-2">
				<section class="about-page">
					{meme}
				</section>
			</div>
    	</div>
	</section> 
<nav>
		<ul class="bar">
			<li class="main-links">
			 <div class="tabs">
				{#each tabs as tab}
   				 <div  id={tab.id} class="tab" class:tab--selected="{selected === tab.id}" on:click={() => {selected = tab.id
					tab.action();
				}}>
      			 	<h2>{tab.label}</h2> 
    			</div>    
				{/each}
			 </div>
			</li>
			<li class="external-links h-stack">
				<img  class="svg" src="/build/images/instagram.svg" alt="instagram">	
				<img  class="svg" src="/build/images/facebook.svg" alt="facebook">
				<img  class="svg" src="/build/images/twitter.svg" alt="twitter">
			</li>
</ul>
</nav>
</header>
<main id="archive">
		<Grid></Grid>
</main>
<footer class="switcher"> 
	<div class="footer-section">
	<h2 class="footer-title">Site Links</h2>
	<ul class="footer-links">
		{#each tabs as tab}
		<li class="footer-link" role="link" on:click={ () => {selected = tab.id; tab.action();}}>
			{tab.label}
		</li>
		{/each}
	</ul>
	</div>
	<div class="footer-section">
		<h2 class="footer-title">Follow Me</h2>
		<div class="h-stack">
				<img  class="svg" src="/build/images/instagram.svg" alt="instagram">	
				<img  class="svg" src="/build/images/facebook.svg" alt="facebook">
				<img  class="svg" src="/build/images/twitter.svg" alt="twitter">	
		</div>
	</div>

</footer>
<div id="bottom-archive"></div>
<style>
	:global(html){
		margin: 0;
		padding: 0;
	}
	:global(body)
{
	margin: 0;
	padding: 0;
	position: relative;
}
:root{
	--max: 80ch;
}
.switcher
{
	padding: 1rem 0;
	display: flex;
	flex-flow: row wrap;
	max-width: var(--max);
	margin: 0 auto;
	justify-content: center;
	text-align: center;
}
.switcher > *{
	flex-grow: 1;
	flex-basis: calc((30rem - 100%) * 999);
}
.svg {
	width: 2rem;
	height: 2rem;
}
.h-stack > * + * {
	margin-left: 0.25rem;
}
.h-stack > * {
	cursor: pointer;
}
img{
	width: 100%;
}
h1{
	font-size: 4rem;
	font-family: 'Abril Fatface';
}
h2{
	font-size: 2rem;
}

header
{
		display: flex;
		flex-direction: column;
		align-items: center;
		height : 99vh;
}

#bottom-archive{
	height: 0;
	width: 0;
}
nav{
		display: flex;
		flex-flow: column;
		flex: 0 0 auto;
		width: 100%;
		position: relative;
}

.bar{
		display : flex;
		margin: 0;
		width: 100%;
		padding: 0;
		list-style: none;
		align-items: center;
		justify-content: center;
	}

.main-links{
		display:flex;
		font-size: 2rem;
		gap: 1rem;
		align-items: center;
		margin-left: auto;
		margin-right: auto;
	}
.footer-section > h2{
	margin-bottom: 0.5rem;
}
main{
		background:#323232;
		width: 100%;
		height: 100%;
	}

.external-links{
	display: flex;
	gap: 1rem;
	position: absolute;
	right: 0;
	display: none;
}
#lollipop{
	height: 50vh;
}
#archive{
	width: 100%;
}
.carousel
{
    display: flex;
    height: 100%;
    box-sizing: border-box;
    overflow: hidden;
}
.slides
{
    transition: transform 0.3s;
    display: flex;
    width: 100%;
}
.slide
{
   flex: 0 0 100%; 
}

.main-page{
	height: 100%;	
	display: flex;
	flex-flow: column nowrap;
	align-items: center;
	justify-content: center;
	/* background-image: url("images/CorinneMain.svg");
	background-size: contain;
	background-position: right bottom;
	background-repeat: no-repeat;
	background-color: #fff9f9; */
}
svg
{
	width: 2rem;
}


.tabs{
    display:flex;
    padding-left: 0.75em;
    padding-right: 0.75em;
    position: relative;
	margin-left: auto;
	margin-right: auto;
}

@media screen and (min-width: 750px){
	.external-links{
		display: block;
	}	
}
.footer-links{
	display: flex;
	justify-content: center;
	gap: 0.25rem;
	flex-direction: row;
}
.footer-link{
	cursor: pointer;
	font-size: 1.2rem;
}
.tab{
    cursor: pointer;
    color: #323232;  
    position: relative;
	transition: background-color 0.3s;
    padding: 1rem;
}

.tab--selected
{
    color: white;
	background: #323232;
}
</style>



