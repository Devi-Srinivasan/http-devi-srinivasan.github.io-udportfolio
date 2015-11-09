Made the following changes.

1.Minified css and js files.(udportfolio/style.css,../views/js/main.js).
2.Added inline css.(index.html,views/pizza.html).
3.Optimized pictures.
4.Modified following ../views/js/main.js code to achieve resize pizza time less than 5ms.
	function changePizzaSizes(size) {
		var i=0;
		var dx = determineDx(document.elementsByClassName("randomPizzaContainer")[i], size);
		var newwidth = (document.elementsByClassName("randomPizzaContainer")[i].offsetWidth + dx) + 'px';	  
		for (var i = 0; i < document.elementsByClassName("randomPizzaContainer").length; i++) {
		  document.elementsByClassName("randomPizzaContainer")[i].style.width = newwidth;
		}
	  }
5. Replaced querySelector with elementsById.
6.Based on innerHeight and innerWidth,modified the code to generate background piizas that will fit within the viewport.
document.addEventListener('DOMContentLoaded', function() {
  var cols = 8;
  var s = 256;
  for (var i = 0; i < 200; i++) {
    var elem = document.createElement('img');
    elem.className = 'mover';
    elem.src = "images/pizza.png";
    elem.style.height = "100px";
    elem.style.width = "73.333px";
    elem.basicLeft = (i % cols) * s;
    elem.style.top = (Math.floor(i / cols) * s) + 'px';
    var phase = Math.sin((document.body.scrollTop / 1250) + (i % 5));
    itemleft = elem.basicLeft + 100 * phase;
	if (itemleft > window.innerWidth){
		continue;
	}
	
	if ((Math.floor(i / cols) * s) > window.innerHeight){
		break;
	}
    document.querySelector("#movingPizzas1").appendChild(elem);
  }
6. Modified code below for pizza.html to run at 60fps.
	   var items = document.getElementsByClassName('mover');
	   var top = document.body.scrollTop;
	   var phases = [];
	   
	   for (var i = 0; i < 5; i++) {
		 phases[i] = Math.sin((top / 1250) + i) * 100;
		}
	   
	   for (var i = 0; i < items.length; i++) {
		items[i].style.left = items[i].basicLeft + phases[i % 5] + 'px';
	  }
7. Added some code at the end of bootstrap to align the contents to fit within the pizzaGenerator.

   