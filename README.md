
//Sarah Brady Bus 353 stopwatch-assignment 1
	
	Titanium.UI.setBackgroundColor('#000000');
	var win = Titanium.UI.createWindow({
	    title:"StopWatch",
	    backgroundColor:"#00FFFF",
	    exitOnClose: true 
	});
	 
	var Stopwatch = Titanium.UI.createView({
	    backgroundColor:"#00FFFF"
	});
	  
	var timer = Titanium.UI.createLabel({
	    text: "00:00:00.0",
	    top: 0,
	    textAlign:"center", 
	    font: { fontSize: 45, fontWeight: 'normal' }, 
	    width: 350,
	 
	});
	 
	var hours = Titanium.UI.createLabel({
	    text: 'Hours',
	    top: 55,
	    left: 60,
	});
	 
	var minutes = Titanium.UI.createLabel({
	    text: 'Mins',
	    top: 55,
	    left: 125,
	});
	 
	var second = Titanium.UI.createLabel({
	    text: 'Secs',
	    top: 55,
	    right: 105,
	});
	 
	var buttonStart = Titanium.UI.createButton({
	   title: 'START',
	   backgroundColor: '#000000',
	   top: 90,
	   left: 40,
	   width: 100,
	   height: 50 
	});
	 
	var buttonReset = Titanium.UI.createButton({
	    title:'RESET',
	    top: 90,
	    right: 40,
	    width: 100,
	    height: 50
	});
	 
	var buttonStop = Titanium.UI.createButton({
	    title:'STOP',
	    backgroundColor: '#000000',
	    top: 150,
	    left: 40,
	    width: 100,
	    height: 50
	});
	
	var started = false;
	var interval = null;
	     
	var _startStopwatch = function() {
	 
		var startTime = new Date();
	 
		var _updateTimer = function updateTimer() {
	    	var unit_hours = 60 * 60 * 1000;
	    	var unit_min = 60 * 1000;
	    	var unit_sec= 1000;
	    	var now = new Date();
	    	var difference = now.getTime() - startTime.getTime();
	    	var hour = Math.floor(difference / unit_hours);
	    	var minute = Math.floor((difference - hour * unit_hours) / unit_min);
	    	var second = Math.floor((difference - hour * unit_min - minute * unit_min) / unit_sec);
	    	var msecond = Math.floor(difference % unit_sec);
	    	timer.text = ('0' + hour).slice(-2) + ':' + ('0' + minute).slice(-2) + ':' + ('0' + second).slice(-2) + '.' + ('00' + msecond).slice(-1);
	    	};
	 
	    intervalid = setInterval(_updateTimer, 0);
	};
	 
	var _stopStopwatch = function() {
	    started = false;
	    clearInterval(intervalid);
	};
	 
	 
	buttonStart.addEventListener("click", function(x){
	    if (started === false && timer.text === '00:00:00.0') {
	        _startStopwatch();
	        started = true;
	      } else if (started === false && timer.text != '00:00:00.0'){
	      	alert ("Press RESET first");
	      }
	});
	 
	buttonReset.addEventListener("click", function(x){
	    if (started === false) {
	        timer.text = '00:00:00.0';
	      } 
	});
	 
	buttonStop.addEventListener("click", function(x){
	    if (started === true){    
	    _stopStopwatch();
	    }
	});
win.add(Stopwatch);
	win.add(buttonStart);
	win.add(buttonReset);
	win.add(buttonStop);
	win.add(timer);
	win.add(hours);
	win.add(minutes);
	win.add(second);
	 
	win.open();
