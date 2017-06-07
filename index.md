<html>
<head>
<meta charset="utf-8"/>
<style>
	body{
		font-size:26px;
	}
</style>
<script>
function Delete() {
    document.getElementById("demo").innerHTML = "";
}

function Show() {
    document.getElementById("demo").innerHTML = "Paragraph";
}
function Test() {
    var xhr = new XMLHttpRequest();
	xhr.open("GET", "https://www.codecademy.com/", false);
	xhr.send();

	console.log(xhr.status);
	console.log(xhr.statusText);
});
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
<button onclick="Delete()">Delete</button>
<button onclick="Show()" >Show</button>
<button onclick="Test()" >test</button>
<br/>
<h1>COUCOU</h1>
<p id="demo"></p>
<hr/>
</body>
</html>
