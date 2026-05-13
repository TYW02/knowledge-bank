Following [YouTube Vid](https://www.youtube.com/watch?v=I2UBjN5ER4s&list=WL&index=4)

| Current Time Stamp | Status | Project Status |
| ------------------ | ------ | -------------- |
| 59:55              | Done   | Do product page, fix mobile              |


Get rid of setupTest.js, logo.svg, appTest.js
Go index.js get rid of Strict mode, service worker
Get rid of index.css

In App.js get rid of everything except the base stuff


Images and videos go into the public folder
## Create components
- Start with NavBar.js and .css
- Create Button.js and .css
- Create HeroSection.js and .css
- Create pages folder and create Home.js

### In NavBar
- Start with rfce
- import react, {useState} from 'react'
- import {Link} from react-router-dom
- create a nav 
- npm install react-router-dom
- create Link home
- const [click, setClick] = useState(false);
----------------------------------------------------------------
Under link tab 
create a div for menu icon
use i with fas fa-times and fas fa-bar to create hamburger menu




## In App.js
- import navbar
- use navbar component
- import { BrowserRouter as Router, Routes, Route}