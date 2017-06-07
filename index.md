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
    var request = require('request');
    request('http://www.google.com', function (error, response, body) {
        console.log('error:', error); // Print the error if one occurred
        console.log('statusCode:', response && response.statusCode); // Print the response status code if a response was received
        console.log('body:', body); // Print the HTML for the Google homepage.
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
