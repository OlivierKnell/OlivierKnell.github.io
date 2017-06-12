<html>
<head>
<meta charset="utf-8"/>
<script>

function createCORSRequest(method, url) {
  var xhr = new XMLHttpRequest();
  xhr.open(method, url, true);
  return xhr;
}

function TestInput(callback) {
	xhr = createCORSRequest("POST", "https://terralego-scraper.herokuapp.com/graphql");
	xhr.responseType = 'json';
	xhr.setRequestHeader("Content-Type", "application/json");
	xhr.setRequestHeader("Accept", "application/json");
	xhr.onload = function () {
	  console.log('data returned:', xhr.response);
	  if (xhr.readyState === 4) {
	    if (xhr.status === 200) {
	      callback(xhr);
	    } else {
	      console.error(xhr.statusText);
	    }
	  }
	}
	var insee = document.getElementById("myInput").value;
	var query = '{result(insee:"' + insee + '"){params' 
	if (document.getElementById("checkResults").checked == true){
		query += ' results';
	};
	if (document.getElementById("checkValueDate").checked == true){
		query += ' valueDate';
	};
	query += '}}';
	xhr.send(JSON.stringify({
	  query: query
	}));
}

function myCallback(xhr){
	var resJson = xhr.response;
	var res = '<pre>' + JSON.stringify(resJson, null, 4) + '</' + 'pre>';
	document.getElementById('resultJ').innerHTML = res;
	showResInTable(resJson);
}

function showResInTable(json){
	var finalResult = "";
	results = json.data.result
	for (var result in results){
		var myResult = "<div><h3>Data : </h3><br/>";
		var params = results[result].params;
		
		myResult += "<table style='width:100%;'><tr><th>Params key</th><th>Params value</th></tr>";
		for (var param in params){
			var key = param;
			var val = params[param];
			myResult += "<tr><td>" + JSON.stringify(key) + "</td><td>" + JSON.stringify(val) + "</td></tr>";
		}
		myResult += "</table>";
		
		if (document.getElementById("checkValueDate").checked == true){
			var dates = results[result].valueDate;
			myResult += "<table style='width:100%;'><tr><th>Date</th><th>" + JSON.stringify(dates) + "</th></tr>";
			myResult += "</table>";
		};
		
		if (document.getElementById("checkResults").checked == true){
			var analytiques = results[result].results.infos_analytiques
			var generales = results[result].results.infos_generales
			
			myResult += "<table style='width:100%;'><tr><th>Generale key</th><th>Generale value</th></tr>";
			for (var generale in generales){
				var key = generale;
				var val = generales[generale];
				myResult += "<tr><td>" + JSON.stringify(key) + "</td><td>" + JSON.stringify(val) + "</td></tr>";
			}
			myResult += "</table>";
			
			myResult += "<table style='width:100%;'><tr><th>Analytique key</th><th>Analytique value</th></tr>";
			for (var analytique in analytiques){
				var key = analytique;
				var val = analytiques[analytique];
				myResult += "<tr><td>" + JSON.stringify(key) + "</td><td>" + JSON.stringify(val) + "</td></tr>";
			}
			myResult += "</table>";
		};
			
		finalResult += myResult;
	}
	document.getElementById("resultT").innerHTML = finalResult;
}

function testRest(callback){
	xhr = createCORSRequest("POST", "https://terralego-scraper.herokuapp.com/api/result_eau/");
	xhr.responseType = 'json';
	xhr.setRequestHeader("Content-Type", "application/json");
	xhr.setRequestHeader("Accept", "application/json");
	xhr.onload = function () {
	  console.log('data returned:', xhr.response);
	  if (xhr.readyState === 4) {
	    if (xhr.status === 200) {
	      callback(xhr);
	    } 
	    else {
	      console.error(xhr.statusText);
	    }
	  }
	}
	xhr.send();
}
</script>
</head>
<body>
	<input id="myInput" type="text" placeholder="code insee here">
	<br/>
	<input type="checkbox" id="checkResults"> I want results<br>
	<input type="checkbox" id="checkValueDate"> I want date<br>
	<button onclick="TestInput(myCallback)" >Apply graphql</button>
	<button onclick="TestRest(myCallback)" >Apply rest</button>
	<br/>
	<div id="resultJson">
		<h2>Result :</h2>
		<p id="resultJ"></p>
	</div>
	<div id="resultTab">
		<h2>Result in table :</h2>
		<div id="resultT"></div>
	</div>
	<div id="resultRest">
		<h2>Result in table :</h2>
	</div>
	<hr/>
</body>
</html>

