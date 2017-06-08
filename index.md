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
	      myCallback(xhr);
	    } else {
	      console.error(xhr.statusText);
	    }
	  }
	}
	var insee = document.getElementById("myInput").value;
	var query = '{result(insee:"' + insee + '"){params results valueDate}}';
	//xhr.callback = callback(xhr);
	xhr.send(JSON.stringify({
	  query: query
	}));
	console.log('test input1');
	callback(xhr, showData);
}

function myCallback(xhr, callback){
	console.log("my callback 1");
	var resJson = xhr.response;
	var res = JSON.stringify(resJson, null, 4);
	document.getElementById("result").innerHTML = res;
	var str = "Date : " + resJson.data.result.valueDate;
	document.getElementById("resultNice").innerHTML = str;
	//showData(resJson);
	console.log("my callback 2");
	callback(resJson);
}

function showData(json){
	var str = "Date : " + json.data.result.valueDate;
	document.getElementById("resultNice").innerHTML = str;
	console.log("show data");
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

