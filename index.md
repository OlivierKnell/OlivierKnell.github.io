<html>
<head>
<meta charset="utf-8"/>
<style>
	body{
		font-size:26px;
	}
</style>
<script>
var request = require('request');
request('http://www.google.com', function (error, response, body) {
  console.log('error:', error); // Print the error if one occurred
  console.log('statusCode:', response && response.statusCode); // Print the response status code if a response was received
  console.log('body:', body); // Print the HTML for the Google homepage.
});
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
<button id="graphbtn">graphique</button>
<br/>
<h1>COUCOU</h1>
<hr/>
</body>
</html>
