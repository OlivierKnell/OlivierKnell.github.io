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
	      callback(xhr, showData);
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

function myCallback(xhr, callback){
	var resJson = xhr.response;
	var res = '<pre>' + JSON.stringify(resJson, null, 4) + '</' + 'pre>';
	document.getElementById("result").innerHTML = res;
	callback(resJson);
}

function showData(json){
	//console.log('data3 : '+ JSON.stringify(json.data.result[0].params));
	/*
	var results = json.data.result
	var str = ""
	for (i = 0; i < results.length; i++){
		str += "\nDate : " + JSON.stringify(results[i].valueDate, null, 4);
		str += '\nParams : ' + '<pre>' + JSON.stringify(results[i].params, null, 4) + '</' + 'pre>';
		//str += "\nResults : " + JSON.stringify(results[i].results);
	}
	document.getElementById("resultNice").innerHTML = str;
	*/
}
</script>
</head>

<body>
<input type="checkbox" id="checkResults"> I want results<br>
<input type="checkbox" id="checkValueDate"> I want date<br>
<input id="myInput" type="text">
<button onclick="TestInput(myCallback)" >get data</button>
<br/>
<h2>Result :</h2>
<p id="result"></p>
<hr/>
</body>
</html>

