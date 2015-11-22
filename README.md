## Website Performance Optimization portfolio project documentation

The /prod directory will hold the changes made for the Web Perf Optimization project (P4). Measurements and results will be documented here. The files are in the gh-pages branch so real-world measurements can be taken.

	Page can be opened at http://hoanger.github.io/P4/prod/

	Files can be found in Github repository: https://github.com/hoanger/P4/tree/gh-pages/prod

### Optimizations for index.html

##Start:
	Pagespeed score: 28 mobile, 28 desktop
	DCL: 142ms, onload: 2635ms
	15 requests, 2.3 MB transferred finish in 2.8 s

1. Reduce and resize image to 100px wide and compress pizzeria.jpg (new file pizzeria100.jpg): reduce bytes
	pizzeria.jpg: 2.3 MB transferred 2.8s
	pizzeria100.jpg: 8.2 KB transferred 170 ms

	Pagespeed score: 76 mobile, 89 desktop
	DCL: 204ms, onload: 602ms
	15 requests, 61.5 KB transferred finish in 737 ms

1. Move analytics script to the end of body and make async: NO CHANGE

1. Inline small CSS files in HTML head to lower server requests: reduce server requests

	Pagespeed score: 77 mobile, 90 desktop
	DCL: 84ms, onload: 309ms
	12 requests, 72.9 KB transferred finish 355 ms

1. Request Google web font via javascript at end of body: shorten CRP

	Pagespeed score: 95 mobile, 96 desktop
	DCL: 15ms, onload: 226ms
	13 requests, 79.9 KB transferred finish 267 ms

### Optimizations for pizza.html - changes to main.js

##Start:
	Time to resize pizzas: Time to resize pizzas: 231.04499999999825ms
	Average time to generate last 10 frames: 44.6649999999996ms

1. Move for loop interator comparison outside in a variable to avoid multiple calls to "document.querySelectorAll(".randomPizzaContainer").length;" in changePizzaSizes function
	Time to resize pizzas: 4.539999999997235ms

1. Move scrollTop calculation, var scrollPos = document.body.scrollTop; outside for loop in updatePositions to be only called once
	Average time to generate last 10 frames: 7.8595000000000255ms

1. Reduced number of sliding pizzas from 200 to 40. My screen resolution only displays 18 at a time.

1. Replace all instances of "ParseInt" with mre efficient "Math.floor" function. Source: https://jsperf.com/math-floor-vs-math-round-vs-parseint/183
	Average time to generate last 10 frames: 0.6399999999996364ms

1. Replaced "document.querySelector/querySelectorAll" with "getElementById" and "getElementsByClassName" Source: http://jsperf.com/getelementbyid-vs-queryselector
	Average time to generate last 10 frames: 0.414000000001397ms

1. Minified to "main.min.js" and resized "pizzeria.jpg" for faster load times and js execution

1. Force hardware acceleration in CSS for moving pizzas. Suggestion from code review. Source: http://blog.teamtreehouse.com/increase-your-sites-performance-with-hardware-accelerated-css

1. Declare variables outside for loops in updatePositions(), and the event listener for DOMContentLoaded on advice from code reviewer.


