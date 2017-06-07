<html>
<head>
<meta charset="utf-8"/>
<style>
	body{
		font-size:26px;
	}
</style>
<script>
function myFunction() {
    document.getElementById("demo").innerHTML = "Paragraph changed.";
}
</script>

</head>
<body>
<select id="ville">
	<option value="toulouse">Toulouse</option>
	<option value="bordeaux">Bordeaux</option>
	<option value="paris">Paris</option>
	<option value="marseille">Marseille</option>
</select>
<button id="meteo">click</button>
<button id="graphbtn" onclick="myFunction()" >graphique</button>
<br/>
<h1>COUCOU</h1>
<p id="demo"></p>
<hr/>
</body>
</html>
