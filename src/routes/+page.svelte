<!-- App.svelte -->
<script>
    ;
    import anime from 'animejs';
    import { afterUpdate } from 'svelte';
    import {onMount} from "svelte";
    import Typewriter from 'svelte-typewriter';
    import Blob from './blob.svelte';
    let LottiePlayer;
	let mainContainer;
    let acceptTerms = false;
    let upperText = "Are you stuck waiting in long queues?";
    let lowerText = "No need to worry!";
    export let data;
    const a ='/static/bg2.jpg';
    let controlsLayout = [];
	const landingPageLottieFile = "threejslandingpage.json";
    const mobilefile= "animat.json";
    onMount(async () => {
		const module = await import('@lottiefiles/svelte-lottie-player');
		LottiePlayer = module.LottiePlayer;
		animateMain();
		// if (data?.animationsLoaded === 'false') {
        //     document.cookie = `animationsLoaded=true; path="/"`;
        // }
	});
    let TN=[];

    onMount(() => {
        TN = data?.records
    });

    let x = 0;
    let y = 0;

    function handleMouseMove(e) {
        x = e.clientX;
        y = e.clientY;
        const rect = e.currentTarget.getBoundingClientRect();
        document.getElementsByClassName(".spot-blur")[0].animate(
                [
                    {
                        top: x,
                        left: y
                    }
                    ,
                    { top: (y-200).toString() + "px",
                      left: (x-300).toString() + "px",
                    }
                ], {
                    duration: 10000,
                    iterations: 1,
                    delay: 400,
                    easing: "cubic-bezier(0.49, 0.47, 0.63, 0.85)",
                } 
            )
        // x = e.clientX - rect.x;
        // y = e.clientY - rect.y;
        // console.log(`x: ${e.clientX - rect.x}, y: ${e.clientY - rect.y}`)
    };

    // const updateAnimationsLoaded = () => {document.cookie = `animationsLoaded=true; path="/"`};

    function animateMain() {
		anime({
		targets: [".dila-denge"],
		translateY: ['-80%', 0],
		rotate: ["-10deg", 0],
		scale: [0, 1],
		opacity: [0, 1],
		easing: 'spring(1, 80, 10, 4)',
		duration: 200,
		delay: 3800
		});

        anime({
		targets: [".everything-else", "header"],
		opacity: [0,1],
		easing: 'easeInSine',
		duration: 1000,
		delay: 4000
		});

        anime({
		targets: [".lottie"],
		opacity: [0,1],
		easing: 'easeInSine',
		duration: 2000,
		delay: 3000
		});	
        anime({
		targets: [".get-started"],
		opacity: [0,1],
		easing: 'easeInSine',
		duration: 500,
		delay: 4000
		});	
	}
    afterUpdate(() => {
		animateMain();
	});
    
    

</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div class="lg:bg-background">
    <nav class="main-container h-[100%] flex justify-center text-center lg:px-16 px-4 dark:bg-gray-950 overflow-hidden lg:overflow-hidden pb-12">
        <Blob></Blob>
        <div class="xl:pt-[350px] pt-[150px] xl:pb-[200px] pb-[100px] flex justify-center items-center xl:gap-40 md:gap-28 select-none xl:flex-row flex-col">
            <div class="flex justify-center items-center flex-col lg:px-0 px-2 gap-2 z-[2]">
                <!-- {console.log(data?.animationsLoaded)} -->
                {#if data?.animationsLoaded === "false"}
                    <Typewriter cursor={true} interval=85 mode="concurrent">
                        <h2 class="lg:text-3xl text-xl select-none text-black/90 font-instrument">
                           {upperText}
                        </h2> 
                    </Typewriter>
                {/if}
                {#if data?.animationsLoaded === "true"}
                    <h2 class="lg:text-3xl text-xl select-none text-black/90 font-instrument">
                        {upperText}
                    </h2> 
                {/if}
                <h2 class="dila-denge bg-gradient-to-r from-gradient1 to-gradient2  text-transparent bg-clip-text text-[44px] lg:text-7xl text-4xl select-none block font-instrument overflow-visible h-[80px] font-[900]">{lowerText}</h2>
                <p class="text-xl get-started max-w-[400px] text-text pb-2">We have an <b>epic solution</b> for you which saves your <i>precious time</i>!</p>
                <a href="/register" class="get-started btn rounded-xl py-1 px-6 bg-gradient1 hover:bg-gradient1/5 hover:text-text hover:border-gradient1 border-1 border-background text-background font-bold">Get Started</a>
                <!-- <button class="know-more mt-4 py-2 px-4 text-xl font-instrument text-text border-2 border-gradient2 hover:bg-gradient2 rounded-xl cursor-pointer">
                    Know More
                </button> -->
                <!-- <p class="font-instrument lg:text-2xl text-md lg:max-w-[650px] max-w-[350px]">Lorem ipsum lorem ipsum lorem ipsum lorem ipsum. Lorem ipsum lorem ipsum lorem ipsum lorem ipsum. Lorem ipsum lorem.</p> -->
            </div>

            
        </div>
    </nav>
    <div class="h-screen"></div>
    <!-- <div class="w-[100%] h-[100%]">
        <div class="lottie absolute xl:left-[calc(50%-700px)] xl:top-[-300px] xl:w-[1400px] xl:translate-x-0 w-screen left-[calc(50%)] translate-x-[-50%] top-[0px] h-auto overflow-hidden xl:block hidden animate-rotateInfinite">
            <lottie-player src={landingPageLottieFile} background="transparent" speed="0.5" direction="1" mode="normal" loop autoplay></lottie-player>
        </div>
        
    </div> -->
    <div class="w-[100%] h-[50%] overflow-hidden">
        <div class="lottie absolute xl:left-[calc(50%-700px)] xl:top-[-300px] xl:w-[1400px] xl:translate-x-0 w-screen left-[50%] translate-x-[-50%] top-[0px] h-[50%] object-cover overflow-hidden xl:hidden block">
            <lottie-player src={mobilefile} background="transparent" speed="0.4" direction="1" mode="normal" loop autoplay></lottie-player>

        </div>
    </div>

    <!-- <div style={`left: ${x}px; top: ${y}px`}  class={`spot-blur absolute w-28 h-28 blur-[50px] rounded-full bg-gradient-to-t from-gradient1 to-gradient2`}>
    </div> -->

</div>
