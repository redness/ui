# Slide Menu
====

Slide menu with 2 anchors

xml

	<Widget id="menu" src="com.imobicloud.slide_menu" anchors="[0, 230]">
			<ListView id="lvMenu" class="menu"></ListView>
			<View id="content" role="slider"/>
		</Widget>

tss

	".menu": { width: 230, top: 40, bottom: 30, left: 0 }
  "#content": { width: '100%', left: 0, backgroundColor: '#fff' }

js

	var items = [];
	for (var i=0; i < 10; i++) {
	  	items.push({
	  		properties: { itemId: 'item_' + i },
	  		title: { text: 'Item title ' + i },
	  		image: { image: '/images/avatar.jpg' }
	  	});
	};

	var sections = [{
		// headerView: Ti.UI.View,
		items: items
	}];

	$.menu.init(sections, {
 		slider: $.content,
 		anchor: [60, 200],
 		defaultAnchor: 0,
 		onClick: menuClicked
	});

	function menuClicked(e){
		// e.itemId
	}

	// toggle menu
	$.menu.toggle();
	$.menu.toggle(1);

You can update menu properties directly via $.menu.menu (this is a ListView)
Example:

	$.menu.menu.getView().top = 100;
	$.menu.menu.addEventListener('delete', function(){});
	$.menu.menu.headerView = $.UI.create('View', { classes: 'menu-header' });

	// custome templates

	var cateTemplate = {
		properties: $.createStyle({ classes: 'slide-menu-item' }),
	    childTemplates: [
	        {
	        	type: 'Ti.UI.View',
	        	properties: $.createStyle({ classes: 'slide-menu-item-wrapper', apiName: 'View' }),
	        	childTemplates: [
	        		{
	        			type: 'Ti.UI.ImageView',
	        			bindId: 'image',
	        			properties: $.createStyle({ classes: 'slide-menu-image', apiName: 'ImageView' })
	        		},
	        		{
	        			type: 'Ti.UI.Label',
	        			bindId: 'title',
	        			properties: $.createStyle({ classes: 'slide-menu-title', apiName: 'Label' })
	        		}
	        	]
	        }
	    ]
	};

	$.cates.menu.applyProperties({
		templates: { 'categoryTemplate': cateTemplate },
		defaultItemTemplate: 'categoryTemplate'
	});

	var items = [];
	for (var i=0; i < 10; i++) {
	  	items.push({
	  		// template: 'categoryTemplate',
	  		properties: { itemId: 'item_' + i },
	  		title: { text: 'Item title ' + i },
	  		image: { image: '/images/avatar.jpg' }
	  	});
	};
