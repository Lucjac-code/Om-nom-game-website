<script>
	let om_nom_y= 620;
	let om_nom_x= -60;
	let no_food= false;
	let no_water= false;
	let no_happy= false;
	let water_value= 100;
	let happiness_value= 100;
	let food_value= 100;
	let bar_values= [food_value,water_value,happiness_value];
	let red_bars= [no_food,no_water,no_happy,];
	let game=false;
	let start_menu=true;
	let game_over=false;
	let game_win= false;
	let eating=false;
	let food=false;
	let candy_y=0;
	
	/*bestämmer om mätarna i spelet ska minska*/
	let bars=true;
	
	let cloud_x=-80;
	
	/*avgör om molnet ska åt höger eller vänster*/
	let right=true;
	
	let left_key=true;
	let right_key=true;
	let candy_invisible=false;
	let rain_drops= [{y:20,x:0},{y:20,x:0},{y:20,x:0}];
	let Jumping=false;
	let can_jump=true;
	let counter=100;
	setInterval(bar_values_reduce, 150);
	setInterval(candy_spawn,100);
	setInterval(candy_move,20);
	setInterval(move_cloud,20);
	setInterval(candy_remove,20);
	setInterval(countdown,1000);
	setInterval(move_drops,50);
	
	function Start(){
		start_menu=false;
		game=true;
	}
	function countdown(){
		if (game==true){
			counter-=1;
			if (counter==0){
				game=false;
				game_win=true;
			}
		}
	
	}
	function game_end(){
		game=false;
		game_over=true;
	}
function bar_values_reduce(){
	if (game==true){
		
		for (let i in bar_values){
			if (bars==true){
				bar_values[i] -=0.25;
				bar_values = bar_values
				}
				if(bar_values[i]==0){
					red_bars[i]=true;
					red_bars= red_bars;
					bars=false;
					setTimeout(game_end,1500);/*man ska hinna se röda mätarna som dyker upp innan game over skärmen*/
				}
				
			}
		}
}


	let M = 1
	let V = 10
	let Rise = 0
	function jump_true(){
		can_jump=true;
	}
	function jump(){
		if (game==true){
			if (om_nom_x==-60){
				if (can_jump==true){
				requestAnimationFrame(Happy);
				can_jump=false;
				setTimeout(jump_true,400);
				}
			}
		}
	}
	async function Happy(){
		Jumping=true;
			for (let x=0;x<21;x++){
				let K = 0.4 * M * V**2  
				om_nom_y -= K 
				V -= 1 
				if (V < 0)
					M = -1 
				if( V == -11){
					M = 1 
					V = 10
					Rise = 0  }
						
		await new Promise(resolve =>setTimeout(resolve,10));
			}
			Jumping=false;
			if (bars==true){
				bar_values[2]+=5;
			}
			if (bar_values[2]>100){
				bar_values[2]=100;
				bar_values=bar_values;
			}	
	}
	function candy_spawn(){
		if (food==false){
			if (om_nom_x==-354 & eating==true){
				candy_y=100;
				candy_invisible=false;
				food=true;
			}
		}
}
	function candy_move(){
		if (food==true){
			candy_y+=2;
		}
		if  (candy_y>190 && candy_y< 200){
			if (eating==true && om_nom_x==-354){
				candy_invisible=true;
				if (bars==true){
					bar_values[0]+=10;
					bar_values=bar_values;
				}
				if (bar_values[0]>100){
						bar_values[0]=100;
						bar_values=bar_values;
				}	
			}
		}

}
	function candy_remove(){
		if (candy_y> 400){
			candy_invisible=true;
			food=false;
		}
	}
	/*variabler som påverkar monstrets y värde i animationerna när den går vänster eller höger*/
	let m = 1
	let v = 10
	let rise = 0
	function move_cloud (){
		if (right==true){
			cloud_x+=2;
			cloud_x=cloud_x;
			if (cloud_x>400){
				right=false;
			}
		}
		if (right==false){
			cloud_x-=2;
			cloud_x=cloud_x;
			if (cloud_x<-280){
				right=true;
			}
		}
			
	}
async function move_drops(){
	for (let i in rain_drops){
		if (rain_drops[i].y <= 25 || rain_drops[i].y > 100){
			if (right==true){
				rain_drops[i].x = cloud_x+40
				rain_drops[i].y = 25
			}
			else{
				rain_drops[i].x = cloud_x+10/*är till för att dropparna ska spawna under molnet*/
				rain_drops[i].y = 25
			}
		}
		if (eating==true){
			if (rain_drops[i].y >82&&rain_drops[i].y<86){
				if (rain_drops[i].x>(om_nom_x-4)&&rain_drops[i].x<(om_nom_x+34)){
					rain_drops[i].x = cloud_x
					rain_drops[i].y = 25
					if (bars==true){
					bar_values[1]+=15;
					bar_values=bar_values;
					}
					if (bar_values[1]>100){
					bar_values[1]=100;
					bar_values=bar_values;
					}	
				}
			}
		}
		rain_drops[i].y +=0.5
		await new Promise(resolve =>setTimeout(resolve,2500));
	}
	rain_drops = rain_drops
}

	async function left_animation(){
			if (om_nom_x>-354){
				for (let x=0;x<21;x++){
				om_nom_x -=2

					console.log(om_nom_y)
					let k = 0.1 * m * v**2  
					om_nom_y -= k 
					v -= 1 
					if (v < 0)
						m = -1 
					if( v == -11){
						m = 1 
						v = 10
						rise = 0  }
				
			await new Promise(resolve =>setTimeout(resolve,10)	);
			}}
			console.log(om_nom_x);
		}
		
	async function right_animation(){
		if (om_nom_x<402){
			for (let x=0;x<21;x++){
				om_nom_x +=2

					console.log(om_nom_y)
					let k = 0.1 * m * v**2  
					om_nom_y -= k 
					v -= 1 
					if (v < 0)
						m = -1 
					if( v == -11){
						m = 1 
						v = 10
						rise = 0  }
				

			await new Promise(resolve =>setTimeout(resolve,10));
			}}
			console.log(om_nom_x);
		}
		
	
	function key_left_true(){
		left_key=true;
	}
	function key_right_true(){
		right_key=true;
	}
	function mouth(){
		eating=!eating;
		
	}

function onKeyDown(e){
	if (game==true){
		if (Jumping==false){
			
			if (left_key==true){
				if (e.keyCode == 37){
					requestAnimationFrame(left_animation);
					left_key=false;
					setTimeout(key_left_true,280);
				}
			}
			if (right_key==true){
				if (e.keyCode == 39){
					requestAnimationFrame(right_animation);
					right_key=false;
					setTimeout(key_right_true,280);
				}
			}
			if (eating==false){
				if (e.keyCode == 38){
					mouth();
					setTimeout(mouth,2500);
				}
			}
		}
	}
}
		
		
	

</script>
	<svelte:window on:keydown|preventDefault={onKeyDown} />
	<main class="background">
		<!-- svelte-ignore a11y-img-redundant-alt -->
		
		<img class="candy-string" src="candy-in-rope.png" alt="picture of candy">
		<img class="Hypno-candy" src="Hypno_Candy.png" alt="">
		{#if start_menu}
			<div class="start-screen">
				<img class="Button-image" src="Button.png" alt="">
				<p class="play" on:click={()=> Start()}>Play</p>
				<img class="Cut_the_rope_logo" src="Cut_the_rope.png" alt="TItle">
				<img class="Tamagotchi" src="tamagotchi.png" alt="">
			</div>
		{/if}
		{#if game_over}
			<div class="game-over">
				<p class=" loose-text" >Game over</p>
				<img class="sad" src="om_nom_sad.png" alt="">
				<img class="flame" style=" "src="Flame.jpg" alt="">
			</div>
		{/if}
		{#if game_win}
			<div class="win-screen">
				<img class="win-picture" src="Win.png" alt="">
				<p class="win-text">Om Nom is pleased</p>
			</div>
		{/if}
		{#if game}
			<div class="game">
			
				<p style="top:8%; position:absolute; left:44%; color:black; font-size:40px;">{counter}</p>
				<img class="Air-cushion" src="Air.png" alt="air cushion" on:click={()=> jump()}>
				<img class="om-nom-eat" class:visible= {eating} style="margin-top:{om_nom_y}px; margin-left:{om_nom_x}px" src="Eating-candy.png" alt="">
				<img class="om-nom" class:hidden_om_nom= {eating} style="margin-top:{om_nom_y}px; margin-left:{om_nom_x}px" src="Om-nom.png" alt="">
				<img class="cloud" src="pngmoln.png" alt="" style="margin-left:{cloud_x}px">
				
				{#if food}
					<img class="candy" style="margin-top:{candy_y}px; {candy_invisible? "visibility: hidden;": ""}" src="Candy.png" alt="candy">
				{/if}
				
				
					{#each rain_drops as {y,x}}
						{#if y > 25}
							<img class="drop" style=" top:{y}%; margin-left:{x}px;"src="rain.png" alt="">
						{/if}
					{/each}
					
				
				
				<div class="candy-box">
					<img src="Candy.png" alt="food" class="food-image">
				</div>
				
				<div class="pipe-start">
					<div class="pipe-end"></div>
				</div>
				
				<div class="platform"></div>
				
				<img class="water-sign" src="water.png" alt="">
				<img class="happines-sign" src="Smily.png" alt="smily">
				<img class="candy-sign" src="candy-emoji.png" alt="candy">
				
				
				<div class= "bar-frame"   style="margin-left:32px;  {red_bars[0]? "visibility: visible;": ""} ">
					<progress class="bar-value" style="height:{bar_values[0]}%" max="100" value>9</progress>
				</div>
				

				<div class= "bar-frame"  style="margin-left:64px; {red_bars[1]? "visibility: visible;": ""}">
					<progress class="bar-value" style="height:{bar_values[1]}%" max="100" value>9</progress>
				</div>
				

				<div class= "bar-frame"  style="margin-left:96px; {red_bars[2]? "visibility: visible;": ""}">
					<progress class="bar-value" style="height:{bar_values[2]}%" max="100" value>9</progress>
				</div>
		
			</div>
		{/if}
	</main>



<style>
	.background{
		display:flex;
		width:100vw;
		height:100vh;
		justify-content:center;
		flex-direction:row;
		background-image: url("/brown-background.jpg")
	}
	.game-over{
		background-color:black;
		width:65vw;
		height:98vh;
		z-index:4;
		display:flex;
		justify-content:center;
		
	}
	.start-screen{
		background-color:rgb(190, 155, 73);
		width:65vw;
		height:98vh;
		display:flex;
		justify-content:center;
	}
	.Cut_the_rope_logo{
		width:20vw;
		height:15vh;
		position:absolute;
	}
	.Tamagotchi{
		height:30vh;
		position:absolute;
		top:4%;
	}
	.Button-image{
		width:30vw;
		height:20vh;
		top:40%;
		position:absolute;
	}
	.play{
		font-size: 30px;
		position:absolute;
		top:48%;
		color:black;
	}
	.game{
		background-image: url("/Cardboard.jpg");
		width:65vw;
		height:98vh;
		position:relative;
		
	}
	.loose-text{
		font-size:50px; 
		margin-top:20px;
		color:red;
	}
	.sad{
		z-index:1;
		width:600px;
		height:600px;
		position:absolute;
	}
	.flame{
		width:65vw;
		height:80vh;
		position:absolute;
		z-index:0;
		bottom:0%;
	}
	.win-screen{
		background-color: rgb(194, 150, 75);
		width:65vw;
		height:98vh;
		justify-content:center;
		z-index: 4;
	}
	.win-picture{
		position:absolute;
		left:28%;
		top:3%;
	}
	.win-text{
		position:absolute; 
		top:80%; 
		left:32%; 
		font-size:60px; 
		color:green;
	}

	progress{

		color:green;
		
	}
	.candy-string{
		height:400px;
		width:200px;
		position:absolute;
		left:2%;
	}
	.Hypno-candy{
		position:absolute;
		height:140px;
		width:140px;
		left:86%;
		top:16%;
	}
	.candy{
		width:3%;
		height:3%;
		position:absolute;
		top:58%;
		left:15.5%;
		z-index: 3;
	}
	.drop{
		position:absolute;
		width:2%;
		height:3%;
		left:50%;
		z-index:3;
		
	}
	
	.cloud{
		display:flex;
		width:100px;
		height:80px;
		left:50%;
		top:20%;
		position:absolute;
	}
	.Air-cushion{
		display:flex;
		position:absolute;
		bottom:2%;
		width:50px;
		height:70px;
		left:50%;
		margin-left: -60px;
		z-index:2;
	}
	.candy-box{
		display:flex;
		height:22%;
		width:9.5%;
		background-color:rgb(194, 150, 75);
		top:64%;
		position:absolute;
		justify-content: center;
	}
	.food-image{
		display:flex;
		height:50%;
		width:50%;
		top:10%;
		position:absolute;
		
	}
	.pipe-start{
		display: flex;
		width:9%;
		height:4%;
		left:9.5%;
		top: 66%;
		position:absolute;
		z-index:5;
		background-color:rgb(133, 128, 128);
		border-top-right-radius: 10px;
	}
	.pipe-end{
		display: flex;
		width:40%;
		height:100%;
		left:60%;
		top: 67%;
		position:absolute;
		z-index:5;
		background-color:rgb(133, 128, 128);
	}
	.water-sign{
		height:30px;
		width:20px;
		margin-left:66px;
		left:10px;
		position:absolute;
		top:1%;
	}
	.happines-sign{
		height:20px;
		width:20px;
		margin-left:96px;
		left:10px;
		position:absolute;
		top:1%;
		rotate:180deg;
	}
	.candy-sign{
		height:30px;
		width:20px;
		margin-left:32px;
		left:10px;
		position:absolute;
		top:1%;
	}
	
	
	
	.bar-frame{
		background-color:red;
		width:20px;
		height:80px;
		border-color:black;
		border-width:2px;
		position:absolute;
		border-radius:10px;
		top: 5%;
		left:10px;
		visibility:hidden;
	}
	.bar-value{
		width:17px;
		background-color: green;
		border-radius:10px;
		bottom: 0%;
		position: absolute;
		visibility:visible;
		
	}
	.platform{
		background-color:rgb(210, 161, 86);
		width:998px;
		height:110px;
		align-self:end;
		position:absolute;
		bottom:0%;
		
	}
	.om-nom-eat{
		display:flex;
		width:5%;
		height:9%;
		left:50%;
		position:absolute;
		z-index: 4;
		visibility:hidden;
	}
	.om-nom{
		
		display:flex;
		width:5%;
		height:9%;
		left:50%;
		position:absolute;
		z-index: 3;
	}
	
	.visible{
		display:flex;
		width:5%;
		height:9%;
		left:50%;
		position:absolute;
		z-index: 1;
		visibility:visible;
	}
	.hidden_om_nom{
		display:flex;
		width:5%;
		height:9%;
		left:50%;
		position:absolute;
		z-index: 1;
		visibility:hidden;
	}
	
</style>