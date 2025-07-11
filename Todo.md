```dataview
TABLE
file.ctime as Created
From #todo 
Sort file.ctime ASC
Limit 20
```


```dataviewjs
if (typeof Chart === 'undefined' || typeof ChartGeo === 'undefined') { const chartScript = document.createElement('script'); chartScript.src = 'https://cdn.jsdelivr.net/npm/chart.js'; chartScript.onload = () => { const geoScript = document.createElement('script'); geoScript.src = 'https://cdn.jsdelivr.net/npm/chartjs-chart-geo'; geoScript.onload = createHeatmap; document.head.appendChild(geoScript); }; document.head.appendChild(chartScript); } else { createHeatmap(); } function createHeatmap() { const daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']; const frequency = Array(7).fill(0); const pages = dv.pages(); pages.forEach(page => { const day = new Date(page.file.ctime).getDay(); frequency[day]++; }); const data = daysOfWeek.map((day, index) => ({ day, value: frequency[index] })); const chart = dv.el("div"); const ctx = dv.el("canvas", {}, chart); ctx.width = 400; ctx.height = 400; new Chart(ctx, { type: 'bar', data: { labels: daysOfWeek, datasets: [{ label: 'Note Creation Frequency', data: frequency, backgroundColor: 'rgba(75, 192, 192, 0.2)', borderColor: 'rgba(75, 192, 192, 1)', borderWidth: 1 }] }, options: { responsive: true, plugins: { legend: { position: 'top', }, title: { display: true, text: 'Note Creation Frequency by Day of the Week' } }, scales: { y: { beginAtZero: true } } } }); }
```

