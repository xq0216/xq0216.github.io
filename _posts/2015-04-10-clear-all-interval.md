---
layout: post
title: clear all intervals
categories: []
tags: [javascript]
published: True

---

JS中一次性清除所有interval（或timeout）：

	var highestIntervalId = setInterval(";");
	for (var i = 0 ; i < highestIntervalId ; i++) {
	    clearInterval(i);
	}

setInterval会返回一个递增的id，然后循环clear所有id对应的interval即可。