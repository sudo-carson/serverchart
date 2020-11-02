# serverchart
Server-sided charts for JavaScript. Forked from the now unmaintained `node-chartjs` package.

## Getting Started

### Peer Dependencies

You'll need to `npm install chart.js` as it is a peer dependency of serverchart.

Also make sure you have installed `canvas`' dependencies ([see installation wiki](https://github.com/Automattic/node-canvas/wiki/_pages))

```
npm i serverchart
```

## Usage
serverchart is just a Node wrapper for [Chart.js](https://www.chartjs.org/). Everything is the exact same, but instead of doing the following normally:
```html
<canvas id="myChart" width="400" height="400"></canvas>
<script>
const ctx = document.getElementById('myChart').getContext('2d');
const myChart = new Chart(ctx, {
	...
});
</script>
```

...you would do this:
```js
const Chart = require('serverchart');
const chart = new Chart(400, 400);
chart.makeChart({ ... }).then(() => {
	chart.drawChart();
	chart.toFile('foo.png');
});
```

Here's a more complete example:
```js
const Chart = require('serverchart');
const chart = new Chart(200, 200); // width and height

chart.makeChart({
	type: 'bar',
	data: {
		labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
		datasets: [{
			label: '# of Votes',
			data: [12, 19, 3, 5, 2, 3],
			backgroundColor: [
				'rgba(255, 99, 132, 0.2)',
				'rgba(54, 162, 235, 0.2)',
				'rgba(255, 206, 86, 0.2)',
				'rgba(75, 192, 192, 0.2)',
				'rgba(153, 102, 255, 0.2)',
				'rgba(255, 159, 64, 0.2)'
			],
			borderColor: [
				'rgba(255, 99, 132, 1)',
				'rgba(54, 162, 235, 1)',
				'rgba(255, 206, 86, 1)',
				'rgba(75, 192, 192, 1)',
				'rgba(153, 102, 255, 1)',
				'rgba(255, 159, 64, 1)'
			],
			borderWidth: 1
		}]
	},
	options: {
		scales: {
			yAxes: [{
				ticks: {
					beginAtZero: true
				}
			}]
		}
	}
})
.then(res => {
	chart.drawChart();
	chart.toFile('test.png');
});
```

serverchart can also write the output image to a buffer; it's just `const buffer = await chart.toBuffer()`.