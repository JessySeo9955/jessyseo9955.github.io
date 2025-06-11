---
layout: post
title:  "[Front-end] Weather Compare - IndexedDB, Web Components"
date:   2025-05-19 20:27:14 -0400
categories: jekyll update
---

## Project
- [[Repository] Weather Compare Frontend](https://github.com/JessySeo9955/indexedDB_weather)
- [[Site] Weather Compare Frontend](https://weather-compare-a1d1e.web.app)
- **IndexedDB** – for local data caching 
- **Service Worker** – for background sync
- **Web Components** – for building reusable, modular UI components

## IndexedDB + Service Worker
<img style="max-width: 100%; border: 1px solid #ddd" src="https://raw.githubusercontent.com/JessySeo9955/indexedDB_weather/main/.github/images/flowchart2.png" />
<img style="max-width: 100%; border: 1px solid #ddd" src="https://raw.githubusercontent.com/JessySeo9955/indexedDB_weather/main/.github/images/flowchart.png" />

## Web Components
```html
<body>
	<div class="container text-body">
	    <div class="row main-section">
	        <country-summary id="local-location" class="col-6"></country-summary>
	        <country-summary id="seoul-location" class="col-6"></country-summary>
	    </div>
	    <div class="row main-section">
	        <daily-weather id="local-hourly" class="col col-6"></daily-weather>
	        <daily-weather id="seoul-hourly" class="col col-6"></daily-weather>
	    </div>
	</div>
</body>
```


## Screenshots
<img style="max-width: 100%; border: 1px solid #ddd" src="https://raw.githubusercontent.com/JessySeo9955/indexedDB_weather/main/.github/images/screenshot_weather.png" />
