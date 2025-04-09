<script>

</script>

	<main class="background">
		<div class="game">
			
			<img class="om-nom" src="Om-nom.png" alt="">
			<div class="platform"></div>
			
			<div class= "bar" style="margin-left:30px">
				<div class="food-value"></div>
			</div>
			
			<div class= "bar" style="margin-left:60px">
				<div class="food-value"></div>
			</div>
			
			<div class= "bar" style="margin-left:90px">
				<div class="food-value"></div>
			</div>
		</div>
	</main>



<style>
	.background{
		display:flex;
		width:100vw;
		height:100vh;
		justify-content:center;
		flex-direction:row;
	}
	.game{
		background-image: url("Cardboard.jpg");
		width:65vw;
		height:98vh;
		position:relative;
		
	}
	.bar{
		width:20px;
		height:70px;
		border-color:black;
		border-width:2px;
		position:absolute;
		border-radius:10px;
		top:0%;
		background-color:green;
		left:10px;
	}
		
	.platform{
		background-color:rgb(210, 161, 86);
		width:998px;
		height:60px;
		align-self:end;
		position:absolute;
		bottom:0%;
	}
	.om-nom{
		margin-top:600px;
		left:0%;
		width:60px;
		height:120px;
		margin-right:400px;
		position:absolute;
	}
</style>