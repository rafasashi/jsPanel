![jsPanel jQuery Plugin](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/readme-header.jpg)

A jQuery Plugin to generate configurable floating panels for use in a backend solution and other web applications.

---

README FILE IS CURRENTLY A WORK IN PROGRESS

### ![Dependencies](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/dependencies.jpg)
+ jQuery version 1.7.0 or greater
+ jQuery UI version 1.9.0 or greater (with at least core, resizable, draggable)
+ HTML5 compatible browser

The most basic way to add a jsPanel to your document is:

	$( selector ).jsPanel();

This will append a jsPanel with all the default options to the first element of the jQuery collection specified by the selector.

### ![API](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/api.png)

The function accepts two optional arguments. A **configuration object** to set all the options of the jsPanel and a **callback function**.

	$( selector ).jsPanel( [ { options } , callback( jsPanel) ] );
	

| OPTIONS        | METHODS          | CALLBACK      |
| -------------- | ---------------- | ------------- |
| id             | title()          | callback()    |
| title          | addToolbar()     |               |
| size           | close()          |               |
| position       | closeChildpanels() |               |
| overflow       | movetoFront()    |               |
| content        | minimize()       |               |
| load           | maximize()       |               |
| ajax           |                  |               |
| contentBG      |                  |               |
| resizable      |                  |               |
| draggable      |                  |               |
| toolbarContent |                  |               |

### ![options](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options.png)

#### ![id](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-id.png)
Type: string | function

Default: as generated by [jQuery.fn.uniqueId](http://api.jqueryui.com/uniqueId/). If .uniqueId() is not available, a function as shown in the second example below is used to set an id.

This option will set the value of the [id attribute](http://www.w3schools.com/tags/att_global_id.asp) of the outermost div element of the jsPanel.

**If the id passed with option.id already exists in the document**, it will be ignored and another id will be generated as described above. The new id will be attached to the title of the jsPanel as a reminder.

**Examples:**

	$( selector ).jsPanel({
		id: 'testpanel'
	});
	
	$( selector ).jsPanel({
		id: function(){ return 'jsPanel_' + ( $('.jsPanel').length + 1 ) }
	});

#### ![title](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-title.png)
Type: string | function

Default: a function building a default string like "jsPanel No 1", "jsPanel No 2", "jsPanel No 3", and so on ...

This option will set the value of the title/header of the jsPanel.

To set an empty title/header use the option with an empty string.

**Examples:**

	$( selector ).jsPanel({
		title: 'Title of the jsPanel'
	});
	
	$( selector ).jsPanel({
		title: function(){ return 'jsPanel No ' + ( $('.jsPanel').length + 1 ) }
	});

#### ![size](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-size.png)
Type: object | function

Default: { width: 600, height: 370 }

This option will set the width and height of the jsPanel in pixels.

**Possible values for width/height:** integer | string | 'auto' | function

+ An **integer** will be interpreted as pixel value
+ A **string** will be parsed using [parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt). If the return value is > 0 it will be used as pixel value
+ **'auto'** will set the width/height depending on the content of the jsPanel
+ width/height also accept a **function** as value. The return value of the function will be parsed using [parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt) and used to set css width/height of the jsPanel if the return values are > 0

**Examples:**

	$( selector ).jsPanel({
		size: {
			width: 500,
			height: 300
		}
	});

	$( selector ).jsPanel({
		size: {
			width: '600px',
			height: 'auto'
		},
		position: { top: 360, left: 300 }
    });
	
	$( selector ).jsPanel({
		size: {
			width: function(){ return $(window).width()/3 },
			height: 350
		}
    });

#### ![position](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-position.png)
Type: object

Default: { top: 'auto', left: 'auto' }

This option will set the position of the jsPanel in pixels relative to the parent element containing the jsPanel. The parent element needs to be positioned somehow for option.position to work properly.

**Possible values for top and left:** integer | string | 'auto' | 'center'

+ An **integer** will be interpreted as pixel value
+ A **string** will be parsed using parseInt() and the result will be used as pixel value
+ **'auto'** will automatically position the jsPanel
+ **'center'** will center the jsPanel within the containing element. 'center' for position.top and/or position.left can not be used when the respective values for size.height/size.width are set to 'auto' (positioning will be automatic in this case)

top/left also accept a **function** as value. The return value of the function will be parsed using [parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt) and used to set css top/left of the jsPanel if the return values are >= 0

**Using 'center' for position.top and/or position.left will be ignored if the respective values for size.height/size.width are 'auto'. In this case position.top and/or position.left will be set to 'auto'.**

**Remember:** Positioning is always relative to the parent element containing the jsPanel, not to the window. So when the containing element is scrolled, the jsPanel might not be visible in the current viewport.

**Examples:**

	// Example setting pixel values for top and left
	$( selector ).jsPanel({
		position: {
			top: 550,
			left: 300
		}
	});
	
	// Example using automatic positioning for top and left
	$( selector ).jsPanel({
		position: {
			top: 'auto',
			left: 'auto'
		}
    });
	
	// Example using automatic positioning for one direction only
	$( selector ).jsPanel({
		position: {
			top: 860,
			left: 'auto'
		}
    });
	
	// Example using horizontal centering
	$( selector ).jsPanel({
		position: {
			top: 915,
			left: 'center'
		}
    });
	
	// This example will not work since there are no fixed values for width and/or height. Results in default positioning.
	$( selector ).jsPanel({
		size: { width: 'auto', height: 'auto' },
		position: { top: 'center', left: 'center' }
    });
	
#### ![overflow](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-overflow.png)
Type: object

Default: { vertical: 'scroll', horizontal: 'scroll' }

This option will set the css [overflow-y](http://www.w3schools.com/cssref/css3_pr_overflow-y.asp) / [overflow-x](http://www.w3schools.com/cssref/css3_pr_overflow-x.asp) properties of the div element containing the content of the jsPanel.

**Possible values for vertical and horizontal:** 'visible' | 'hidden' | 'scroll' | 'auto' | 'initial' | 'inherit'

**Example:**

	$( selector ).jsPanel({
		overflow: {
			vertical: 'scroll',
			horizontal: 'hidden'
		}
    });
	
#### ![content](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-content.png)
Type: string | function | jQuery object

Default: there is no default content

This option is one of several ways to fill the content area of the jsPanel. It's a good way to add content if you have only a small piece of html to insert or can pass a function. Other options to add content are **option.load**, **option.ajax** and the **callback function**.

**Examples:**

	// Adding an image with a simple html string
	$( selector ).jsPanel({
		content: "<img src='js/jsPanel/images/pl.gif' alt=''>"
    });
	
	// Adding an image using a function
	$( selector ).jsPanel({
		content: function(){ return "<img src='js/jsPanel/images/pl.gif' alt=''>"; }
    });
	
	// Adding an image with a named function
	var func = function(){ return "<img src='js/jsPanel/images/pl.gif' alt=''>"; }
    $( selector ).jsPanel({
		content: func
    });
	
	// Adding a jQuery object (that can even be chained)
	$( selector ).jsPanel({
		content: $( '<p>Lorem ipsum ...</p>' ).css( {padding:'20px', 'text-align':'center'} )
    });	
	
#### ![load](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-load.png)
Type: object

Default: there is no default for this option

The keys/values of the option.load configuration object are used in the same way as the arguments for jQuery .load() would be used.

**Possible values for url, data and complete:**


+ **url:** A string containing the URL to which the request is sent.
+ **data:** A plain object or string that is sent to the server with the request.
+ **complete:** A callback function that is executed when the request completes.

**For detailed information about the jQuery .load() configuration refer to the [jQuery API](http://api.jquery.com/load/).**

**Examples:**

	// Adding content with option.load
    $( selector ).jsPanel({
		load: {
			url: 'files/example-load.html',
			complete: function(){ console.log( "It's done!" ) }
		}
    });
	
#### ![ajax](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-ajax.png)
Type: object

Default: there is no default for this option

The keys/values of the option.ajax configuration object are used in the same way as the arguments for jQuery.ajax() would be used.

**For detailed information about the jQuery.ajax() configuration refer to the [jQuery API](http://api.jquery.com/jQuery.ajax/).**

**Examples:**

	// Adding content with option.ajax
    $( selector ).jsPanel({
		ajax: {
			url: 'files/example-ajax.html'
		}
    });

#### ![contentBG](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-contentBG.png)
Type: string | object

Default: is set in the css file _jsPanel.css_

This option will set the css properties of only the jsPanel content div.

**Passing a string** will use this string as value for the css [background](http://www.w3schools.com/cssref/css3_pr_background.asp) property like [.css( 'background', string )](http://api.jquery.com/css/)
**Passing an object** will use this object like [.css( object )](http://api.jquery.com/css/)

**Examples:**

	//Changing css background-color using a string
	$( selector ).jsPanel({
		contentBG: '#234567'
    });
	
	// Changing more than one css background property using a string
	$( selector ).jsPanel({
		contentBG: 'url("background.png") repeat scroll 0 0 #567890'
    });
	
	// Changing multiple css properties using an object
	$( selector ).jsPanel({
		contentBG: {
			color:'#FFFFFF',
			background:'#234567'
		}
    });

#### ![resizable](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-resizable.png)
Type: object

Default: The [jQuery-UI resizable](http://jqueryui.com/resizable/) interaction is enabled on all jsPanels with the following options:

    {
		containment: 'document',
		autoHide: false,
		minWidth: 150,
		minHeight: 100
    }
	
You can change the resizable options to your needs by adding them to the configuration object of the jsPanel. Let's say you want to change the [containment](http://api.jqueryui.com/resizable/#option-containment) to "parent" and add [maxWidth](http://api.jqueryui.com/resizable/#option-maxWidth) and [maxHeight](http://api.jqueryui.com/resizable/#option-maxHeight) values. You could do it like this:

    $( selector ).jsPanel({
		resizable: {
			containment: 'parent',
			maxWidth: 800,
			maxHeight: 600
		},
		position: { top: 260, left: 260 }
    });
	
This will change the "containment" option and add values for the maxWidth/maxHeight options of the jQuery-UI resizable interaction while preserving the other default options.

For detailed information on how to use the jQuery-UI resizable interaction see the [api documentation](http://api.jqueryui.com/resizable/)

#### ![draggable](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-draggable.png)
Type: object

Default: The [jQuery-UI draggable](http://jqueryui.com/draggable/) interaction is enabled on all jsPanels with the following options:

    {
		handle: 'div.jsPanel-hdr',
		containment: 'document',
		stack: '.jsPanel',
		opacity: 0.6
    }
	
You can change the draggable options to your needs by adding them to the configuration object of the jsPanel. Let's say you want to add a callback to the stop event. You could do it like this:

    $( selector ).jsPanel({
		draggable: {
			stop: function( event, ui ) {
					ui.helper.css( 'background', '#235849' );
			}
		},
		position: { top: 250, left: 300 }
    });
	
This will change the background color of the jsPanel itself after dragging is finished.

For detailed information on how to use the jQuery-UI draggable interaction see the [api documentation](http://api.jqueryui.com/draggable/)

#### ![toolbarContent](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/options-toolbarContent.png)
Type: string

Default: there is no default toolbarContent

This option allows to add a toolbar to the jsPanel header. Using this option will automatically add a div element to the jsPanel header and appends the passed html string to this div element.

**Example:**

    $( selector ).jsPanel({
		toolbarContent: '<p>Toolbar content goes here ...</p>'
    });

### ![methods](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/methods.png)

#### ![title\( \[ true | string \] \)](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/method-title.png)
Gets or sets the title of an already existing jsPanel

**title\(\)** Returns the html element containing the title text when used without an argument

    var jspanel = $( selector ).jsPanel({
        title: 'Title of jspanel'
    });
    console.log( jspanel.title() );

**title\( true \)** Returns the title text when used with one argument which is _true_

    var jspanel = $( selector ).jsPanel({
        title: 'Title of jspanel'
    });
    console.log( jspanel.title( true ) );

**title\( string \)** Returns the jsPanel and sets the title to string when used with one argument which is a string

    var jspanel = $( selector ).jsPanel({
        title: 'Title of jspanel'
    });
    console.log( jspanel.title( 'And this is a new title!' ) );


#### ![addToolbar\( string \)](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/method-addToolbar.png)
Adds a toolbar to an already existing jsPanel in the same way the **option.toolbarContent** does and returns the jsPanel

    var jspanel = $( selector ).jsPanel({
        title: 'Title of jspanel'
    });
    console.log( jspanel.addToolbar( '<p>toolbar content ...</p>' ) );

#### ![close\(\)](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/method-close.png)
Removes the jsPanel from the DOM and returns the the element that contained the jsPanel

This method accepts no arguments

    var jspanel = $( selector ).jsPanel({
        position: { top: 70, left: 300 }
    });
    console.log( jspanel.close() );

#### ![closeChildpanels\(\)](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/method-closeChildpanels.png)
Removes all childpanels of a jsPanel from the DOM and returns the jsPanel the childpanels were removed from

This method accepts no arguments

    // generate a parent panel and store it in a variable
    var testpanel = $( selector ).jsPanel({
        id: 'jspanel',
        position: { top: 70, left: 320 }
    });
    // generate a childpanel within the content area of testpanel
    $( ".jsPanel-content", testpanel ).jsPanel({
        position: { top: 'center', left: 'center' },
        size: { width: 250, height: 150 }
    });
    // remove the childpanel
    console.log( testpanel.closeChildpanels() );

#### ![movetoFront\(\)](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/method-movetoFront.png)
Moves a jsPanels to the front by increasing the z-index and returns the jsPanel

This method accepts no arguments

    // generate a few jsPanels
    var testpanel1 = $( selector ).jsPanel( { position: { top:70, left:360 } } ),
        testpanel2 = $( selector ).jsPanel( { position: { top:95, left:385 } } ),
        testpanel3 = $( selector ).jsPanel( { position: { top:120, left:410 } } );

    // move testpanel1 to the front
    console.log( testpanel1.movetoFront() );

#### ![minimize\(\)](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/method-minimize.png)
Minimizes a jsPanel to the lower left corner of the browser viewport

This method accepts no arguments

    // generate a jsPanel
    var testpanel = $( selector ).jsPanel( { position: { top:70, left:360 } } );

    // minimize testpanel1
    console.log( testpanel.minimize() );

#### ![maximize\(\)](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/method-maximize.png)
Maximizes or normalizes a jsPanels depending of the current status of the jsPanel and returns the jsPanel

This method accepts no arguments

A **normalized jsPanel** (meaning it's visible at it's specified position and with it's specified size) will be maximized within its parent element.

A **minimized or maximized jsPanel** will be restored to its latest normalized status.

    // generate a jsPanel
    var testpanel = $( selector ).jsPanel( { position: { top: 100, left: 360 } } );

    // execute the maximize method on the childpanel several times
    console.log( childpanel.maximize() );

### ![callback](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/callback.png)

#### ![callback\( jsPanel \)](https://github.com/Flyer53/jsPanel/raw/master/demopage/images/method-callback.png)
A callback function that is executed when the jsPanel is inserted in the document. **The function receives the jsPanel as argument.**

**Examples:**

    // Get the id attribut of the jsPanel
    $( selector ).jsPanel( {
        position: { top: 60, left: 300 }
    }, function( panel ){
        console.log( panel.attr( 'id' ) )
    });

    // Load content using the native jQuery.load() method
    $( selector ).jsPanel( function( panel ){
        $( '.jsPanel-content', panel ).load( 'files/callback-2.html' );
    });

    // Change title, find content area, load content using the native jQuery.load() method
    $( selector ).jsPanel( {}, function( panel ){
        panel
        .title( 'Welcome Panel' )
        .find( '.jsPanel-content' )
        .load( 'files/callback-3.html' );
    });
