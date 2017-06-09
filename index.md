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
	document.getElementById("resultJ").innerHTML = res;
	showResInTable(resJson);
}

function showResInTable(json){
	var finalResult = ""
	for (var result in json.data.result){
		var myResult = "<div><h3>Data : </h3><br/>";
		myResult += "<table>";
		for (var param in result.params){
			var key = param;
			var val = result.params[param];
			myResult += "<tr><td>" + key + "</td><td>" + val + "</td></tr>";
		}
		myResult += "</table>";
		finalResult += myResult;
	}
	document.getElementById("resultT").innerHTML = finalResult;
}

function testRest(){
	xhr = createCORSRequest("POST", "https://terralego-scraper.herokuapp.com/api/result_eau/");
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
	xhr.send();
}
</script>
</head>

<body>
<input id="myInput" type="text" placeholder="code insee here">
<br/>
<input type="checkbox" id="checkResults"> I want results<br>
<input type="checkbox" id="checkValueDate"> I want date<br>
<button onclick="TestInput(myCallback)" >Apply</button>
<br/>
<div id="resultJson">
<h2>Result :</h2>
<p id="resultJ"></p>
</div>
<div id="resultTab">
<h2>Result in table :</h2>
<div id="resultT"></div>
</div>
<hr/>
</body>
</html>

