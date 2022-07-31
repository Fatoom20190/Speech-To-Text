# Speech-To-Text
<!DOCTYPE html>

<html lang='ar'>

<head>

    <title>Live Update</title>

    <meta charset="UTF-8">

    <script type="text/javascript" src="autoUpdate.js"></script>

		<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

</head>

<style>

.hidden{

	display:none;

	}

</style>

<bodyid="full">

<div id="liveData" style="display: none;">

    <p>Loading Data...</p>

</div>

<audio id="audio">

	<source  id="sound" src="1.mp3" type="audio/mp3">

</audio>

<audio id="audio2">

	<source  id="sound" src="2.mp3" type="audio/mp3">

</audio>

<p id="demo" style="display:none;"></p>

<script>

  

window.addEventListener('load', function()

{

	var x = document.getElementById("audio"); 

	var x2 = document.getElementById("audio2"); 

	var xhr = null;

	

    getXmlHttpRequestObject = function()

    {

        if(!xhr)

        {               

            // Create a new XMLHttpRequest object 

            xhr = new XMLHttpRequest();

        }

        return xhr;

    };

    updateLiveData = function()

    {

        var now = new Date();

        // Date string is appended as a query with live data 

        // for not to use the cached version 

        var url = 'r1s1.php?' + now.getTime();

        xhr = getXmlHttpRequestObject();

        xhr.onreadystatechange = evenHandler;

        // asynchronous requests

        xhr.open("GET", url, true);

        // Send the request over the network

        xhr.send(null);

    };

    function evenHandler()

    {

        // Check response is ready or not

        if(xhr.readyState == 4 && xhr.status == 200)

        {

            dataDiv = document.getElementById('liveData');

            // Set current data text

            dataDiv.innerHTML = xhr.responseText;

			var xx=xhr.responseText;

			//alert(xx);

			if(xx==1){

    

				x.play();

				output.classList.add("hidden");	

				var y = document.getElementById("audio").duration;

				y=(y*1000);

				console.log(y);

				document.getElementById("demo").innerHTML = y;

				document.getElementById("p1").style.display = "block";

				document.getElementById("p2").style.display = "none";

				setTimeout(function(){ document.getElementById("p1").style.display = "none"; document.getElementById("p2").style.display = "block";}, y);

				

				const Http = new XMLHttpRequest();

				Http.open("GET","https://s-m.com.sa/r1/r1m2.php");

				Http.send();		

				setTimeout(function(){ stt(); }, y);

			}

			document.getElementById("sound").src=xhr.responseText;

            // Update the live data every 1 sec

            setTimeout(updateLiveData(), 10000);

        }

		

    }

	

	

	function stt(){

	

	

		// get output div reference

		var output = document.getElementById("output");

		// get action element reference

		var action = document.getElementById("action");

        // new speech recognition object

        var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;

        var recognition = new SpeechRecognition();

            

        // This runs when the speech recognition service starts

        recognition.onstart = function() {

            action.innerHTML = "<small>listening, please speak...</small>";

        };

                

        recognition.onspeechend = function() {

            action.innerHTML = "<small>stopped listening</small>";

            recognition.stop();

			

recognition=lang.'ar'

					  

        }

              

        // This runs when the speech recognition service returns result

        recognition.onresult = function(event) {

            var transcript = event.results[0][0].transcript;

			var confidence = event.results[0][0].confidence;

            output.innerHTML = "<b></b> " + transcript;

			

			

            output.classList.remove("hidden");

			

			const Http = new XMLHttpRequest();

			Http.open("GET","https://s-m.com.sa/r1/e.php?e=" + transcript);

			Http.send();		

				x2.play();

				var yy = document.getElementById("audio2").duration;

				yy=yy*1000;

				console.log(yy);

				document.getElementById("demo").innerHTML = yy;

				document.getElementById("p1").style.display = "block";

				document.getElementById("p2").style.display = "none";

				setTimeout(function(){ document.getElementById("p1").style.display = "none"; document.getElementById("p2").style.display = "block";}, yy);	

				//output.classList.add("hidden");				

			
