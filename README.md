# Dynamic Paginator (jQuery) - Fast AJAX Paginator using jQuery

##### Listing in a Table

![Listing in a Table](https://raw.githubusercontent.com/alameenlr/dynamic-paginator-jquery/main/rmd-imgs/table.gif)

##### Custom Listing

![Custom Listing](https://raw.githubusercontent.com/alameenlr/dynamic-paginator-jquery/main/rmd-imgs/cats.gif)

Dynamic Paginator(jQuery), or DynamicPaginator is a jQuery JavaScript Library. It is fast library to do pagination in your web applications. DynamicPaginator(jQuery) needs only *total items count*, *counts per page* and *data URL* to fetch the data, It will generate a pagination view for you. You can use custom templates, styles suitable for your Purpose.
  

https://github.com/alameenlr/dynamic-paginator-jquery

  

# Basic usage

### Installation
  

For the latest version:

  

```html
<script src="https://cdn.jsdelivr.net/npm/jquery@3.7.1/dist/jquery.min.js"></script>
<script  src="https://cdn.jsdelivr.net/gh/alameenlr/dynamic-paginator-jquery/dist/dynamic-paginator.min.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/alameenlr/dynamic-paginator-jquery/dist/dynamic-paginator.min.css"/>
```

For a custom one:

```html
<script src="https://cdn.jsdelivr.net/npm/jquery@3.7.1/dist/jquery.min.js"></script>
<script  src="https://cdn.jsdelivr.net/gh/alameenlr/dynamic-paginator-jquery/dist/1.0.0/dynamic-paginator.min.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/alameenlr/dynamic-paginator-jquery/dist/1.0.0/dynamic-paginator.min.css"/>
```

  

### Basic Usage

The next step is to reference the dynamic-paginator's script

```html
<script src="https://cdn.jsdelivr.net/npm/jquery@3.7.1/dist/jquery.min.js"></script>
<script  src="js/dynamic-paginator.min.js"></script>
<link rel="stylesheet" href="css/dynamic-paginator.min.css"/>

...

<body>

<div  id="dynamic-paginate-element"></div>

...

</div>

```

You can now instantiate a new DynamicPaginator object:
```javascript
$("#dynamic-paginate-element").dynamicPaginator({
	search:false,
	loadListURL:"http://127.0.0.1:8000/invoices/list",
	itemProperties:[
		{"key":"id", "label":"Id"},
		{"key":"name", "label":"Name"},
		{"key":"emailid", "label":"Email Address"},
		{"key":"address", "label":"Address"},
		{"key":"date", "label":"Date"},
		{"key":"phone_number", "label":"Phone No"}
	],
	indexedItemPropertiesKeys:["id","name","emailid","address","phone_number"],
	items:[],
	totalItemsCount:10000,
	countsPerPage:10,
	currentViewValues:{
		pageNo:1
	},
	paginationBlock:{
		jumpTo:true
	},
	userParamListner:false,
});
```

## Dynamic Paginator  Options
  
Options to customize dynamic-paginator are passed as the first argument to the `dynamicPaginator` jQuery function.

**Options**: 
| Name | Required | Type | Description |
|:--|:--:|--|:--|
| `getInfoURL` | *yes* | `string` | Basic information to set the view. |
| `loadListURL` | *yes* | `string` | URL to listing the content |
| `itemProperties` | *yes* | `object[]` | Items properties.`{key, label}` |
| `totalItemsCount` | *yes* | `integer` | Total number of Items. |
| `search` |  | `false` or `object` | Search bar Disable, or Setup Search Box |
| `colorTheme` |  | `string` | `auto`, `dark` or `light` Color Theme. (Default:`auto`)|
| `loadedListIsComplete` |  | `boolean` | First Response of the `loadListURL` that contain entire items to paginate. |
| `itemsIndexKey` |  | `string` | Index number key of the item(auto append). |
| `httpRequestHeaders` |  | `object` | Custom Header to `XHR` requests by paginator.  |
| `indexedItemPropertiesKeys` |  | `string[]` | *array of keys* of indexed item properties. |
| `items` |  | `object[]` | List of items to paginate. |
| `maxPagerNumbers` |  | `int` | Number of page-navigator(page no) button shown in pagination section. |
| `setCountsPerPage` |  | `int[]` | List number of items `min` to `max` per page. |
| `pushToHistory` |  | `boolean` | *Default:`true`*, It will push the pageview values to browser history. |
| `showViewingStatus` |  | `boolean` | *Default:`true`*, Current viewing status of the paginator *Eg: Showing 1 to 10 of 200 items*. |
| `currentViewValues` |  | `object` | Current page view status of paginator. |
| `fromStartOnSort` |  | `boolean` | *Default:`true`*, View will be jumped to `1st` page while sorted. |
| `dpParamKeys` |  | `object` | Mapping names of params for page view. |
| `clientSideSearch` |  | `boolean` | *Default:`true`*, Searching in indexed items properties using JavaScript `RegExp`. |
| `clientSideSearchFormat` |  | `string` | *Default: `%{{search-key}}%`*, Searching format. |
| `userParamListener` |  | `boolean` | Reload the page view while user custom input fields updated. |

*Modifying Paginator default View Elements*
| Name | Type | Description |
|:--|:--:|:--|
| `viewTemplate` | `string` | Pagination block template `HTML Body`. |
| `paginationBlock` | `object` | Component(s) of pagination block of Paginated element. |
| `pageContentLoader` | `string` | Custom content loader `HTML Body`. |
| `makeItemPropertyLabel` | `callback fn();` | Function to generate item label like table head. |
| `makeItem` | `callback fn();` | Function to generate items list. |
| `makeViewingStatus` | `callback fn();` | Function to viewing status. |
| `makeSearchBox` | `callback fn();` | Function to generate `Search Box` in paginator. |
| `makeCountSelection` | `callback fn();` | Function to generate `Counts per Page` selection in paginator. |

**Options Description**
 - **`getInfoURL`**: `string`
Default:`null`, Basic information to set the view. URL to load the content, **Response** of the URL must be `JSON` with the keys of DynamicPaginator's **Options**. DynamicPaginator will merge from this URL the response with options use to initiate the paginator. You must add an URL if You want to enable search.

	*Request Body Sample:*
	```javascript
	//Shown in JSON Object actual request body is x-www-form-urlencoded
	{
		"page-no"		: 10,
		"offset"		: 180
		"count"			: 20,
		"order-by"		: "{{Selected Indexted Item Property to Sort}}",
		"order-by-in"	: "asc || desc",
		"search-in"		: "{{Selected Indexted Item Property to Search}}",
		"search-key"	: "{{Key to Perform Search}}",
		"user-params"   : {
			// Client Side Inputs fields with class (dynamic-paginator-input)
			// for more view the sample file(s)
		},
	}
	```

 - **`loadListURL`**: `string`
Default:`null`, URL to listing the content, Response must be `JSON` array.
*Request Body Sample:*
	```javascript
	//Shown in JSON Object actual request body is x-www-form-urlencoded
	{
		"page-no"		: 10,
		"offset"		: 180
		"count"			: 20,
		"order-by"		: "{{Selected Indexted Item Property to Sort}}",
		"order-by-in"	: "asc || desc",
		"search-in"		: "{{Selected Indexted Item Property to Search}}",
		"search-key"	: "{{Key to Perform Search}}",
		"user-params"		: {
			// Client Side Inputs fields with class (dynamic-paginator-input)
			// for more view the sample file(s)
		},
	}
	```
	Response Body Sample:
	``` javascript
	// Response in JSON array of Object with key Items.
	[
		{
			"productName": "XY Air Conditioner"
			"productId": 15457642351,
			...
		},
		{
			"productName": "XY LED Telivision"
			"productId": 14542346446,
			...
		}
		...
	]
	```


 - **`itemProperties`**: `object[]`
List the Item properties here. `{key, label}`, *key* is the property key, *label* is the label of the property.
*Sample:*
	```javascript
    [
        {"key": "name","label": "Name"},
        {"key": "age","label": "Age"},
        {"key": "dob","label": "Date of Birth"},
        ...
    ],
	```

 - **`totalItemsCount`**:`integer`
Default:`0`, How many items in the list to paginate.

 - **`search`**: `false|object`
Default:`{"placeholder":"Search"}`, `false` means search option is disabled.
    - `placeholder`: `string`, Placeholder of the search box.
    - `disabledItemPropertiesKeys`: `string[]`, Array of indexed properties that don't want in search cases.

 - **`colorTheme`**: `auto|dark|light`
Default:`auto`, `auto` The color-appearance will be based on user theme preference.

 - **`loadedListIsComplete`**: `boolean`
Default:`false`, `true` - First Response of the `loadListURL` that contain entire items to paginate, will not send any request to get the content.

 - **`itemsIndexKey`**:`false` or `string`
`false` - disabled. `string` - Enabled, Paginator append the index number of the items in the contents list. It will help you numbering the items especially in table listing case.

 - **`httpRequestHeaders`**: `Object{}`
You can add custom headers to append the `POST` request(s) send by DynamicPaginator.
Eg: `httpRequestHeaders:{'X-CSRF-TOKEN':  "EWhAhSaA6wFEmtOk33ZTMqn0uwuMzHWEnbxgRegO"}`

 - **`indexedItemPropertiesKeys`**: `string[]`
List the indexed item properties here. Properties are key fields to *sort*, or *search* the items in the list.

 - **`items`**:`Object[]`
List of items to paginate. You can also load it from URL. `loadListURL` Response will set as value of `items`.

 - **`maxPagerNumbers`**: `int`
Default:`10`, How many page-navigator button shown in pagination section. You can set the size as you needed.
`maxPagerNumbers:8` will generate pagination block like this `<< 1 2 3 8 ... 10 >>`

 - **`setCountsPerPage`**: `int[]`
Default: `[10,20,50,100,250,500,1000]`, Set count select option values to set maximum items per page.

 - **`pushToHistory`**:`boolean`
Default: `true`, If it is true then, any input changed to set the pageview will be added to browser history. If the your *go-back* the view automatically changed to previous view.

 - **`showViewingStatus`**: `boolean`
Default: `true`, If it is true then, Page viewing status will be added on `{{viewingStatus}}` section in  `viewTemplate`. You can customize the viewing status set `makeViewingStatus` function.

 - **`currentViewValues`**: `Object{}`
Default: `{pageNo:1,count:10}`, Set current page view status of paginator.
	```javascript
	{
		pageNo		:  1,		// number
		count		:  10,		// number
		orderBy		:  "",		// string
		orderByIn	:  "asc",	// string asc, or desc
		searchIn	:  "",		// string
		searchKey	:  "",		// string
		userParams	:  {},		// Object
	}
	```

 - **`fromStartOnSort`**: `boolean`
Default: `true`, If it is true then, View will be jumped to `1st` page while sorted.

 - **`dpParamKeys`**: `{}`
Default value shown here, This will be the parameter names of in the view page URL, `POST` Request body of `getInfoURL`, and `loadListURL`.
	```javascript
	{
		pageNo		:  "page-no",		// string
		count		:  "count",			// string
		orderBy		:  "order-by",		// string
		orderByIn	:  "order-by-in",	// string asc, or desc
		searchIn	:  "search-in",		// string
		searchKey	:  "search-key",	// string
		userParams	:  "user-params",	// Object
	}
	```

 - **`clientSideSearch`**: `boolean`
Default: `true`, If it is `true` and `totalItemsCount < currentViewValues.count` then the searching will be done in the client side. Using JavaScript `RegExp` with the pattern given in `clientSideSearchFormat`.

 - **`clientSideSearchFormat`**:`string`
Default: `%{{search-key}}%`, `%`- represents any characters. `{{search-key}}` the key will placed here. For example, you can do the search start with the key, like this `{{search-key}}%`.

 - **`userParamListener`** : `boolean`
Default: `true`,  If it is `true` then, The page view will reloaded with new updated parameter(s).

#### Managing Paginator View Elements
 - **`viewTemplate`**: `string`
You can set the pagination block template as per your use case. Default template uses *bootstrap* template
Default value shown here.
    `{{countsPerPage}}`, `{{searchBox}}`, `{{propertiesLabel}}`, `{{viewingStatus}}`, `{{itemsList}}`, `{{paginationContent}}` are the variable sections in the paginator. It'll be replaced by the paginator after initialized.
    :warning: *Don't forget to keep the variable section `{{itemsList}}`, `{{paginationContent}}` in the elements.*
	```html
	<div class="d-flex w-100 justify-content-between py-2">
		<div>{{searchBox}}</div>
		<div>{{countsPerPage}}</div>
	</div>
	<table class="w-100">
		<thead>
			<tr>{{propertiesLabel}}</tr>
		</thead>
		<tbody>{{itemsList}}</tbody>
	</table>
	<div class="d-flex w-100 justify-content-between py-2">
		<div class="show-status">{{viewingStatus}}</div>
		<div>{{paginationContent}}</div>
	</div>
	```

 - **`paginationBlock`**: `Object{}`
    You can customize the component(s) of pagination block of Paginated element.
	- `hideOnSinglePage`: `boolean` when the pagination block is hidden when if total pages count is 1.
	- `jumpTo`: `boolean` Enable or, Disable Jump to section in pagination block.
	- `size`: `default || large` Pagination block size.
	- `template`: `Object{}` content element templates of pagination block.
			:warning: *Don't forget to keep the variable section `{{url}}`,  `{{pageNo}}` in the elements.*
		- `pageNumber`: `string` Template of `page-number` button element.  
		- `previous`: `string` Template of `previous` button element.
		- `next`: `string` Template of `next` button element.
		- `more`: `string` Template of `more` button element.
		- `jumpTo`: `string` Template of `jumpTo` section content.
	```javascript
    // This is default
	{
	    hideOnSinglePage:true,
	    jumpTo:false,
	    size:"default",
	    template : {
	        pageNumber:`<a href="{{url}}" class="page-number">{{pageNo}}</a>`,
	        previous:`<a href="{{url}}" class="page-previous">`+
	            `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512"><path d="M9.4 233.4a32 32 0 0 0 0 45.3l192 192a32 32 0 0 0 45.3-45.3L77.3 256 246.6 86.6a32 32 0 0 0-45.3-45.3l-192 192z" fill="currentColor"/></svg>`+
	        `</a>`,
	        next:`<a href="{{url}}" class="page-next">`+
	            `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512"><path d="M310.6 233.4a32 32 0 0 1 0 45.3l-192 192a32 32 0 0 1-45.3-45.3L242.7 256 73.4 86.6a32 32 0 0 1 45.3-45.3l192 192z" fill="currentColor"/></svg>`+
	        `</a>`,
	        more:`<a class="page-more">...</a>`,
	        jumpTo: `<form action="#">`+
	            `<div class="d-flex border jump-to-box">`+
	                `<input type="number" name="jump-to-page" class="lrs-dpf no-border no-outline no-bg number">`+
	                `<button type="submit" class="no-border no-outline no-bg">Go</button>`+
	            `</div>`+
	        `</form>`,
	        background:false,
	    }
	}
	```

 - **`pageContentLoader`**: `string`
	Dynamic paginator have a default loader content if you can set a new loader here. `HTMLText`

 - **`makeItemPropertyLabel`**: `function(property, isIndexed, sorted):string{}`
    DynamicPaginator will iterate this function to generate item label like table head.
	- `property`: `Object{key,label}` List item property .
		- `key`: `string` key of the item Property.
		- `label`: `string` label of the item Property (display name).
	- `isIndexed`: `boolean` If it is in the list `indexedItemPropertiesKeys`.
	- `sorted`: `false | "asc" | "desc"` It is not sorted by on `this` key then `false`
	```javascript
	// This is default
	function(property, isIndexed, sorted){
		if(isIndexed)
			return  `<th tabindex="0" role="columnheader button" data-property-key="${property.key}" class="head-sort${sorted?' '+sorted:''}"${sorted?` title=" Sort `+(sorted=="asc"?"descending":"ascending")+`"`:''}>${property.label}</th>`;
		return  `<th data-property-key="${property.key}">${property.label}</th>`;
	}
	```

 - **`makeItem`**: `function(item, itemProperties, searchedIndex="", searchedKey=""):string {}`
	DynamicPaginator will iterate this function to generate items list.
	- `item`: `Object{}` Item from `loadListURL` response.
	- `itemProperties`: `string[]` Items properties defined in DynamicPaginator.
	- `searchedIndex`: `string[]` Which property key is used to sort the view page.
	- `searchedKey`: `string[]` Search key.
    ```javascript
    // This is default
    function (item, itemProperties, searchedIndex="", searchedKey=""){
        let escapeQuotes = (str) => str?.toString().replace(/[\"]/gm, "&quot;").replace(/[\']/gm, "&apos;");
        let searchMatch = (content)=>{
            let matchRex = new RegExp("("+searchedKey.replace(/[\[\]\/\{\}\(\)\*\+\?\.\\\^\$\|]/g, "\\$&")+")","gui");
            return content.toString().replace(matchRex,"<span class='search-match'>$1</span>")
        }
        return `<tr>`+
            (showItemNumber===false?"":`<td>${itemIndex+1}</td>`)+
            itemProperties.map(p=>
                searchedIndex==p.key?
                (`<td data-key="${p.key}" data-value="${escapeQuotes(item[p.key])}">${searchMatch(item[p.key]??'')}</td>`):
                (`<td data-key="${p.key}" data-value="${escapeQuotes(item[p.key])}">${item[p.key]??''}</td>`)
            ).join('')+
        `</tr>`;
    }
    ```

 - **`makeViewingStatus`**: `function(pageno, countsPerPage, totalItemsCount):string {}`
    Customize viewing status Text. This will set content in `{{viewingStatus}}` Section.
    - `pageno`: `number` Current page number.
	- `countsPerPage`: `number` Items count per page.
	- `totalItemsCount`: `number` Total number of items.
    ```javascript
    // This is default
    function (pageno, countsPerPage, totalItemsCount){
        //Showing 1 to 10 of 52 entries
        if(totalItemsCount==0)
            return "0 entries"
        let to = pageno*countsPerPage;
        let from = to-countsPerPage+1;
        return `Showing ${from} to ${to>totalItemsCount?totalItemsCount:to} of ${totalItemsCount} entries`;
    }
    ```

 - **`makeSearchBox`**: `function(option):string {}`
    Set search box element. This will set content in `{{searchBox}}` section in `viewTemplate`.
    - `option`: `Object{}` Dynamic Paginator Option.
    ```javascript
    // This is default
    function (options){
        let search_sel = ``;
        options.itemProperties.forEach(p=>{
            search_sel += (
                options.indexedItemPropertiesKeys.indexOf(p.key)>-1 && 
                options.search.disabledItemPropertiesKeys.indexOf(p.key)<0
            )
            ?`<option value="${p.key}" ${options.currentViewValues.searchIn==p.key?' selected':''}>${p.label}</option>`:``;
        })
        return `<form action="#">`+
            `<div class="d-flex border search-box">`+
                (search_sel.length>0?`<select name="${options.dpParamKeys.searchIn}" class="no-border no-outline no-bg">`+search_sel+`</select>`:``)+
                `<input type="text" name="${options.dpParamKeys.searchKey}" placeholder="${search_op.placeholder}" class="lrs-dpf no-border no-outline no-bg" value="${options.currentViewValues.searchKey??''}">`+
                `<button type="submit" class="no-border no-outline no-bg"><svg width="18" height="14" style="fill:currentColor;opacity:0.3;" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path d="M416 208c0 45.9-14.9 88.3-40 122.7l126.6 126.7c12.5 12.5 12.5 32.8 0 45.3s-32.8 12.5-45.3 0L330.7 376c-34.4 25.2-76.8 40-122.7 40C93.1 416 0 322.9 0 208S93.1 0 208 0s208 93.1 208 208zM208 352a144 144 0 1 0 0-288 144 144 0 1 0 0 288z"/></svg></button>`+
            `</div>`+
        `</form>`;
    }
    ```

 - **`makeCountSelection`**: `function(fieldname,countsPerPage, totalItemsCount, countSelect):string {}`
    Customize viewing status Text. This will set content in `{{countsPerPage}}` Section.
    - `fieldname`: `string`, Name of select field.
    - `countsPerPage`: `number`, Number of list items in a page.
    - `totalItemsCount`: `number`, Number of items in the list.
    - `countSelect`: `number[]`, List allowed items-count in a page.
    ```javascript
    // This is default
    function (fieldname, countsPerPage, totalItemsCount, countSelect){
        let search_sel = ``;
        countSelect.forEach(n=>{
            search_sel += `<option value="${n}" ${n==countsPerPage?' selected':''}>${n}</option>`;
        })
        return `<div class="set-view-count">`+
            `<select name="${fieldname}" class="lrs-dpf border no-bg no-outline">`+search_sel+`</select>`+
            `<span> Items per page.</span>`+
        `</div>`;
    }
    ```

## Dynamic Paginator Methods
 - **`reload()`**
Reload the entire pagination element based on current view values.
    ```javascript
    var $dpg = $("#paginate").dynamicPaginator(option);

    // This will reload the pagination element based on current view values
    $dpg.refresh();
    ```

 - **`reloadList()`**
Reload items based on current view values. Checking pagination options before loading. 
*Sample case if list count updation is required*.
    ```javascript
    // Setting view value
    $dpg.reloadList();
    ```

 - **`setViewValues(pageNo, count, orderBy, orderByIn, searchIn, searchKey)`**
To set current view values of the paginator. 
*Sample case: Paginator update current values to get list of items property `name` that contain keyword `alam` in `ascending` order  in page number `5`(with `10` items per page)*
    ```javascript
    // Setting view values 
    $dpg.setViewValues(5, 10, "name", "asc", "name", "alam");
    ```

 - **`refreshList()`**
Reload the pagination element content based on current view values. 
    ```javascript
    // Refreshing view content section based on current view values with out checking pagination option update.
    $dpg.refreshView();
    ```

## Custom Inputs Paginator

It's possible when you use custom `viewTemplate`. Create input html elements with class `dynamic-paginator-input` on your custom template. Value of these input fields will kept on `userParams` as an object with `name` of the input as key. **`userParamListener`** is `true` the view list will automatically reload whenever an `input` event triggered by the `dynamic-paginator-input` elements.
    Sample:
```html
<div class="d-flex w-100 justify-content-between py-2">
    <div>{{searchBox}}</div>
    <div>{{countsPerPage}}</div>
</div>
<input type="text" value="my paginator input 1" name="my-custom-input-1" class="dynamic-paginator-input">
<input type="text" value="my paginator input 2" name="my-custom-input-2" class="dynamic-paginator-input">
<input type="text" value="my paginator input 3" name="my-custom-input-3" class="dynamic-paginator-input">
<table class="w-100">
    <thead>
        <tr>{{propertiesLabel}}</tr>
    </thead>
    <tbody>{{itemsList}}</tbody>
</table>
<div class="d-flex w-100 justify-content-between py-2">
    <div class="show-status">{{viewingStatus}}</div>
    <div>{{paginationContent}}</div>
</div>
```

*Request Body Sample:*
```javascript
//Shown in JSON Object actual request body is x-www-form-urlencoded
{
    "page-no"		: 10,
    "offset"		: 180
    "count"			: 20,
    "order-by"		: "{{Selected Indexted Item Property to Sort}}",
    "order-by-in"	: "asc || desc",
    "search-in"		: "{{Selected Indexted Item Property to Search}}",
    "search-key"	: "{{Key to Perform Search}}",
    "user-params"   : {
        "my-custom-input-1" : "my paginator input 1",
        "my-custom-input-2" : "my paginator input 2",
        "my-custom-input-3" : "my paginator input 3"
    },
}
```

## Events
*All the events triggered with variables `event`, and `current view values`.*
Sample event listener:
```javascript
/*
    Sample cvv Object: 
    {
        pageNo		:  1,
        count		:  10,
        orderBy		:  "age",
        orderByIn	:  "asc"
        searchIn	:  "name"
        searchKey	:  "alam"
        userParams	:  {
            "my-custom-input-1": "my paginator input 1",
            "my-custom-input-2": "my paginator input 2",
            ...
        }
    }
*/
$("#dynamic-paginate-element").on('page-loaded', function(e,cvv) {
    // do for page-loaded
});
```
 - **`page-loaded`**
Event triggered when page content loaded.

 - **`next-click`**
Event triggered when next page button clicked.

 - **`prev-click`**
Event triggered when previous page button clicked.

 - **`count-change`**
Event triggered when view per Page count Updated.

 - **`sorted`**
Event triggered when sorted view sorted.

 - **`info-load-error`**
Event triggered while error in Paginator Info Loading.

 - **`page-load-error`**
Event triggered while error in Paginator Page Content Loading.