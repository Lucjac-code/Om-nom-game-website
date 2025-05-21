<script>
	let om_nom_y= 620;
	let om_nom_x= -60;
	let food_value= 100;
	let no_food= false;
	let no_water= false;
	let no_happy= false;
	let water_value= 100;
	let happiness_value= 100;
	let bar_values= [food_value,water_value,happiness_value];
	let red_bars= [no_food,no_water,no_happy];
	let game=true;
	let pressed=false;
	let eating=false;
	let food=false;
	let candy_y=0;
	let bars=true;
	let cloud_x=-80;
	let right=true;
	let left_key=true;
	let right_key=true;
	let up_key=true;
	let candy_invisible=false;
	let rain=false;
	let rain_drops= [{name:"drop", value:false}]
	setInterval(bar_values_reduce, 60);
	setInterval(candy_spawn,100);
	setInterval(candy_move,20);
	setInterval(move_cloud,20);
	setInterval(candy_remove,20);
	// up = 38
      // down = 40
      // right = 39
      // left = 37
	function bar_values_reduce(){
		if (game==true){
			
				for (let i in bar_values){
					if (bars==true){
						bar_values[i] -=0.5;
						bar_values = bar_values
						}
						if(bar_values[i]==0){
							red_bars[i]=true;
							red_bars= red_bars;
							bars=false;
						
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
	function candy_move(){
		if (food==true){
			candy_y+=2;
		}
		if  (candy_y>190 && candy_y< 220){
			
			if (eating==true && om_nom_x==-354){
				candy_invisible=true;
				/*styling ändras inte när invisible blir false*/
				/*lägg till att godisförsvinner om om nom inte tar den*/
				/*fixa att godis kan försvinna för tidigt*/
			}


			

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
	let m = 1
	let v = 10
	let jump = 0
	/**/
	
	function move_cloud (){
		if (right==true){
			cloud_x+=2;
			if (cloud_x>400){
				right=false;
			}
		}
		if (right==false){
			cloud_x-=2;
			if (cloud_x<-500){
				right=true;
			}
		}
			
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
						jump = 0  }
				
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
						jump = 0  }
				

			await new Promise(resolve =>setTimeout(resolve,10));
			}}
			console.log(om_nom_x);
		}
		
	
	function key_left(){
		left_key=true;
	}
	function key_right(){
		right_key=true;
	}
	function key_up(){
		up_key=true;
	}

	function onKeyDown(e){
		if (game==true){
			if (left_key==true){
				if (e.keyCode == 37){
					requestAnimationFrame(left_animation);
					left_key=false;
					setTimeout(key_left,280);
				}
			}
				
				
				
			}
			if (right_key==true){
				if (e.keyCode == 39){
					requestAnimationFrame(right_animation);
					right_key=false;
					setTimeout(key_right,280);
			}
			}
			/*while key press*/
			if (eating==false){
			if (e.keyCode == 38){
			mouth();
			setTimeout(mouth,2500);
				
			}
				
			}
			}
			
		
		
	
	function mouth(){
		eating=!eating;
		
	}
	
	
</script>
	<svelte:window on:keydown|preventDefault={onKeyDown} />
	<main class="background">
		<!-- svelte-ignore a11y-img-redundant-alt -->
		
		<img class="candy-string" src="candy-in-rope.png" alt="picture of candy">
		<img class="Hypno-candy" src="Hypno_Candy.png" alt="">
		{#if game}
		<div class="game">
			
			
			<img class="Air-cushion" src="Air.png" alt="air cushion">
			<img class="om-nom-eat" class:visible= {eating} style="margin-top:{om_nom_y}px; margin-left:{om_nom_x}px" src="Eating-candy.png" alt="">
			<img class="om-nom" class:hidden_om_nom= {eating} style="margin-top:{om_nom_y}px; margin-left:{om_nom_x}px" src="Om-nom.png" alt="">
			<img class="cloud" src="pngmoln.png" alt="" style="margin-left:{cloud_x}px">
			{#if food}
				
				<img class="candy" style="margin-top:{candy_y}px; {candy_invisible? "visibility: hidden;": ""}" src="Candy.png" alt="candy">
			
			{/if}
			{#if rain}
				{#each rain_drops as drop}
					<img src="rain.png" alt="">
				{/each}
				
			{/if}
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
		background-image: url("brown-background.jpg")
	}
	.game{
		background-image: url("Cardboard.jpg");
		width:65vw;
		height:98vh;
		position:relative;
		
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
		z-index: 2;
		visibility:hidden;
	}
	.om-nom{
		
		display:flex;
		width:5%;
		height:9%;
		left:50%;
		position:absolute;
		z-index: 1;
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