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
  xhr.open(method, url, true);
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
	xhr.onload = function () {
	  console.log('data returned:', xhr.response);
	}
	var insee = document.getElementById("myInput").innerHTML
	document.getElementById("demo").innerHTML = "test ok"
	var query = '{result(insee:"09042"){params results}}';
	xhr.send(JSON.stringify({query: query}));
}

function TestInput() {
	xhr = createCORSRequest("POST", "https://terralego-scraper.herokuapp.com/graphql");
	xhr.responseType = 'json';
	xhr.setRequestHeader("Content-Type", "application/json");
	xhr.setRequestHeader("Accept", "application/json");
	xhr.onload = function () {
	  console.log('data returned:', xhr.response);
	}
	var insee = document.getElementById("myInput").value;
	document.getElementById("demo").innerHTML = "test input :" + insee;
	var query = '{result(insee:"' + insee + '"){params results}}';
	xhr.send(JSON.stringify({
	  query: query
	}))
        var resJson = xhr.response
	var res = JSON.stringify(resJson);
	document.getElementById("result").innerHTML = res;	
}
</script>

</head>
<body>
<button onclick="Delete()">Delete</button>
<button onclick="Show()" >Show</button>
<input id="myInput" type="text">
<button onclick="TestInput()" >test input</button>
<button onclick="Test()" >test</button>
<br/>
<h1>COUCOU</h1>
<p id="demo"></p>
<h2>result</h2>
<p id="result"></p>
<hr/>
</body>
</html>

