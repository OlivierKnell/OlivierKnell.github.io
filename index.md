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
	var query = '{result(insee:"' + insee + '"){params results valueDate}}';
	xhr.send(JSON.stringify({
	  query: query
	}));
}

function myCallback(xhr, callback){
	var resJson = xhr.response;
	var res = '<pre>' + JSON.stringify(resJson, null, 4) + '</' + 'pre>';
	document.getElementById("result").innerHTML = res;
	var str = "Date : " + resJson.data.result.valueDate;
	document.getElementById("resultNice").innerHTML = str;
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
<input id="myInput" type="text">
<button onclick="TestInput(myCallback)" >get data</button>
<br/>
<h2>result raw</h2>
<p id="result"></p>
<h2>result nice</h2>
<p id="resultNice"></p>
<hr/>
</body>
</html>

