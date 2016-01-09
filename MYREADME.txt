#My github repository : https://github.com/Devi-Srinivasan/udportfolio 
(Forked from https://github.com/cameronwp/udportfolio)

Link to my website: devi-srinivasan.github.io/udportfolio

Made the following changes on the original to make it work efficiently.

1.Minified css and js files.(udportfolio/style.css,../views/js/main.js).
2.Added inline css.(index.html,views/pizza.html).
3.Optimized pictures.
4.Modified following ../views/js/main.js code to achieve resize pizza time less than 5ms.
	function changePizzaSizes(size) {
		var i=0;
		var elemen=document.elementsByClassName("randomPizzaContainer");
		var dx = determineDx(document.elementsByClassName("randomPizzaContainer")[i], size);
		var newwidth = (document.elementsByClassName("randomPizzaContainer")[i].offsetWidth + dx) + 'px';	  
		for (var i = 0; i < elemen.length; i++) {
		  elemen[i].style.width = newwidth;
		}
	  }
5. Replaced querySelector with getElementsById.
6.Using innerHeight calculated the no of rows and changed the number of times the loop has to executed.
document.addEventListener('DOMContentLoaded', function() {
 var cols = 8;
  var s = 256;
  var pizza = document.getElementById("movingPizzas1");
  var elem = document.createElement('img'); 
  var row = (Math.floor(window.innerHeight/100))	;
  for (var i = 0; i < (cols*row); i++) {
    var basicLeft = (i % cols) * s;
    elem.className = 'mover';
    elem.src = "images/pizza.png";
    elem.style.height = "100px";
    elem.style.width = "73.333px";
    elem.basicLeft = basicLeft;
    elem.style.top = (Math.floor(i / cols) * s) + 'px';
    pizza.appendChild(elem);
  }
  
  updatePositions();
});
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
7. Added backface-visibilty and transform to mover class.	  
7. Added some code at the end of bootstrap to align the contents to fit within the pizzaGenerator.


   
