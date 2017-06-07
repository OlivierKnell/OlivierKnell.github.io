<html>
<head>
<meta charset="utf-8"/>
<style>
	body{
		font-size:26px;
	}
</style>
<script>
function createCORSRequest(method, url) {
  var xhr = new XMLHttpRequest();
  if ("withCredentials" in xhr) {
    xhr.open(method, url, true);
  } else if (typeof XDomainRequest != "undefined") {
    xhr = new XDomainRequest();
    xhr.open(method, url);
  } else {
    xhr = null;
  }
  return xhr;
}

function Delete() {
    document.getElementById("demo").innerHTML = "";
}

function Show() {
    document.getElementById("demo").innerHTML = "Paragraph";
}

function Test() {
	xhr = createCORSRequest("POST", "https://terralego-scraper.herokuapp.com/graphql");
	xhr.responseType = 'json';
	xhr.setRequestHeader("Content-Type", "application/json");
	xhr.setRequestHeader("Accept", "application/json");
	xhr.setRequestHeader("Access-Control-Allow-Origin", "*");
	xhr.onload = function () {
	  console.log('data returned:', xhr.response);
	}
	var query = '{result(insee:"09042"){params results}}';
	xhr.send(JSON.stringify({
	  query: query
	}));
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

