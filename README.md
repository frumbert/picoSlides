picoSlides
==========

A fork of http://github.com/hqcasanova/picoSlides. See that repo for setup and documentation

Purpose of this fork
--------------------

This code differs in that it has a new public method `$inst.gotoSlide(index)` which allows you to externally direct the presentation to a particular slide.


Example
-------

```javascript
    var init = {
    	index: 2,
    	timestamp: 14											// slide to start on
    };
	var h = document.querySelector("body").offsetHeight,
		w = (h/3) * 4,
		p = $("#slides").picoSlides({
			imgMaxWidth: w,
			startAt: init.timestamp,							// show this slide first
			loadFirst: function (elem) {
				if (init.timestamp > 2) {
					p.picoSlides("gotoSlide", init.timestamp);	// method to go to this slide after first slide loads
				}
			},
			skipBTitle: "",										// if empty, do not show
			skipFTitle: "", 									// if empty, do not show
			linkUrl: false,
			holderTheme: false,
			apiUrl: "//www.slideshare.net/api/oembed/2?url=",
			afterSlideChange: function (obj, page) {			// after a slide changes, emit an event somewhere
				parent.dispatchEvent(new CustomEvent("statuschange", {detail:{index:init.index, slide: page[0], total: page[1]}}));
			}
		});
```


License
-------

All code is licensed under the [MIT License](http://opensource.org/licenses/MIT). In essence, use and modify at your own peril and leave the copyright header intact.