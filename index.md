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
    var xmlHttp = new XMLHttpRequest();
    xmlHttp.open("POST", 'https://terralego-scraper.herokuapp.com/graphql?query={result(insee: "09042") {params results}}', true);
    xmlHttp.send(null);
    console.log(xmlHttp.status);
    console.log(xmlHttp.statusText);
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
