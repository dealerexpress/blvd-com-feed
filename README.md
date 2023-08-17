<img width="220" src="img/logo.svg"><br>
# BLVD.com Inventory Feed Guidelines
Vehicle inventory feed specifications for sending an automated feed to BLVD.com



Add a Brandl Mobility credit app to any site using the javascript loader. Simply copy a few lines into your site and that's it. The module is less than 2kb gzipped minified and has zero dependencies.

**Requires that your site is listed at brandlmobility.com.** If you're not already listed at [brandlmobility.com](https://www.brandlmobility.com), contact us and see about getting your mobility dealership listed. No additional security measures within your own site are required.

### Next Step
Share this page with your [webmaster](#columns) . Below are the technical installation and usage instructions.

-----

<br><br>

# Installation

Everything you need is hosted on a CDN and may be used as shown. Use of the CDN hosted script recommended to ensure our changes get reflected at your site.

### Step 1
Decide where the links/buttons should appear on your site and add standard HTML links. Often this is on a single vehicle for sale page, somewhere near the vehicle price. 

IE:
```html
<a href="/whatever/im/replaced" class="my-app-selector">Apply For A Loan</a>
```
The link can be anything you like. Feel free to wrap images, containers or other elements in an **&lt;a&gt;**. While elements such as div, span, img, etc; will work directly, some browsers may block the clicks.  So just wrap whatever in a standard link or button tag.

-----
### Step 2
Place the following script loader on any page containing links/buttons for the financing application.  *You may place this in an include file such as your footer, allowing use on any page of your site.*
```html
<script src="https://storage.googleapis.com/dx-cdn-public/dx-shared/browser-scripts/brandl-mobility-app-loader/v1/bundle.min.js"></script>

<!-- Initialize a basic loader on any page where links/buttons to the application are 
     desired.  The following should be anywhere AFTER the script loader. -->
<script type="application/javascript">
var basicExample = new BrandlAppLoader({  
   selector: 'a.my-app-selector' 
});
</script>

```

In our basic example, submissions include the dealer information and ensures correct assignment.  Optionally, you may include vehicle information. Continue reading to learn how.

-----
### Step 3
Verify things are working by loading a page in your browser and clicking one of your links.  It should open a window with the application.  The dealer's name should be listed in the header directly under "Brandl obility Application".

### What Next
You can include a <a href="#parameter-vehicle"><code>vehicle</code></a> `object` in the <a href="#parameter-initializer"><code>initializer</code></a> parameter or add/update vehicle information via the <a href="#method-setVehicle">setVehicle()</a> method. 


<br><br>
# Debug
If things are not working correctly, see the javascript console as errors will be displayed to help solve the issue. In Google Chrome, right click the page and choose 'Inspect'.




<br><br>
# Demos
Take a look at a few common use working examples.
<ul>
     <li><a href="https://storage.googleapis.com/dx-cdn-public/dx-shared/browser-scripts/brandl-mobility-app-loader/v1/examples/1_basic.html" target="_blank">Basic without vehicle</a></li>
     <li><a href="https://storage.googleapis.com/dx-cdn-public/dx-shared/browser-scripts/brandl-mobility-app-loader/v1/examples/2_include-vehicle.html" target="_blank">Include vehicle data</a></li>
     <li><a href="https://storage.googleapis.com/dx-cdn-public/dx-shared/browser-scripts/brandl-mobility-app-loader/v1/examples/3_add-vehicle.html" target="_blank">Update vehicle using setVehicle()</a></li>
</ul>




<br><br>

# API Reference

## Constructors

### - BrandlAppLoader(<a href="#parameter-initializer">initializer</a>)
@param <a href="#parameter-initializer"><code>initializer</code></a><br>
Used to initialize the loader.  Make sure you call it using 'new'
```javascript 
// Usage
var myRef = new BrandlAppLoader(initializer);
```
<br><br>

## Methods

<a name="method-setVehicle"></a>
### - setVehicle(<a href="#parameter-vehicle">vehicle</a>)
@param <a href="#parameter-vehicle"><code>vehicle</code></a><br>
Add or update the vehicle associated with application. This is useful if your site's page does not reload between vehicle views. The <a href="#parameter-vehicle"><code>vehicle</code></a> object may also be passed in the <a href="#parameter-initializer">`initializer`</a> object.
```javascript 
// Usage
myRef.setVehicle(vehicle);
```

### - getVehicle()
@returns <a href="#parameter-vehicle"><code>vehicle</code></a><br>
Get the current <a href="#parameter-vehicle"><code>vehicle</code></a> `object`. 
```javascript 
// Usage
myRef.getVehicle();
```

### - resetVehicle()
Clear current set vehicle. 
```javascript 
// Usage
myRef.resetVehicle();
```

### - open()
Open the apply window with current settings. If already open, bring to focus. 
```javascript 
// Usage
myRef.open();
```

### - getElements()
@returns list of elements on the page that have been activated. 
```javascript 
// Usage
myRef.getElements();
```




<br><br>
<a name="parameter-initializer"></a>
## Delivery Methods
<table>
  <thead>
       <tr>
      <th align="left">Name</th>
      <th align="left">Type</th>
      <th align="left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td valign="top"><code>selector</code></td>
      <td valign="top">string</td>
      <td valign="top"><strong>Required</strong>. The selector to find your elements on the page created in step 1. You might find it best to assign a class to each link/button that is only used for selecting and is separate from styles. All elements matching the provided selector will be modified to open/continue filling out a credit app. Internally, we use <a href="https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll" target="_blank">document.querySelectorAll()</a> to find elements matching provided selector string.</td>
    </tr>
    <tr>
      <td valign="top"><a href="#parameter-vehicle"><code>vehicle</code></a></td>
      <td valign="top">object</td>
      <td valign="top">An object with information about the vehicle being applied for. <a href="#parameter-vehicle">See vehicle definition</a></td>
    </tr>
  </tbody>
</table>


<br><br>
<a name="columns"></a>
## Columns/Fields
<table>
  <thead>
     <tr>
       <th align="left">Name</th>
       <th align="left">Key</th>
       <th align="left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td valign="top">Dealer ID (DX)</td>
      <td valign="top"><code>dealerid</code></td>
      <td valign="top">Unique dealer id assigned by Dealer Express API. For multiple location dealers, this is the same for each location.</td>
    </tr>
    <tr>
      <td valign="top">Zip Code</td>
      <td valign="top"><code>zip</code></td>
      <td valign="top">Vehicles location zip code. We use this to match inventory to the correct dealer location.</td>
    </tr>
    <tr>
      <td valign="top">VIN</td>
      <td valign="top"><code>vin</code></td>
      <td valign="top"><strong>*Required*</strong> 17 Digit VIN Number.</td>
    </tr>
    <tr>
      <td valign="top">Year</td>
      <td valign="top"><code>year</code></td>
      <td valign="top">1999, 2008, Etc.</td>
    </tr>
    <tr>
      <td valign="top">Make</td>
      <td valign="top"><code>make</code></td>
      <td valign="top">Ford, Dodge, Toyota, Etc.</td>
    </tr>
    <tr>
      <td valign="top">Model</td>
      <td valign="top"><code>model</code></td>
      <td valign="top">F-150, Mustang, Fiesta, Etc.</td>
    </tr>
    <tr>
      <td valign="top">Trim</td>
      <td valign="top"><code>trim</code></td>
      <td valign="top">SE, SXT, Limited, Etc.</td>
    </tr>
    <tr>
      <td valign="top">New/Used (Chassis)</td>
      <td valign="top"><code>newused</code></td>
      <td valign="top"><strong>*Required*</strong> Chassis New or Used condition</td>
    </tr>
    <tr>
      <td valign="top">Conversion New/Used</td>
      <td valign="top"><code>conversionnewused</code></td>
      <td valign="top"><strong>*Required*</strong> Conversion New or Used condition</td>
    </tr>
    <tr>
      <td valign="top">Conversion Name</td>
      <td valign="top"><code>conversion</code></td>
      <td valign="top">Vehicle Mobility Conversion Name. A combined conversion manufacturer and model. IE: BraunAbility Entervan XT</td>
    </tr>
    <tr>
      <td valign="top">Stock Number</td>
      <td valign="top"><code>stock</code></td>
      <td valign="top"><strong>*Required*</strong> 4584B, 45215</td>
    </tr>
    <tr>
      <td valign="top">List Price</td>
      <td valign="top"><code>price</code></td>
      <td valign="top">19900, 28000, All non numeric characters will be striped. All characters after a period (.) will be stripped. $19,900.99 --> 19900</td>
    </tr>
    <tr>
      <td valign="top">Exterior Color</td>
      <td valign="top"><code>ecolor</code></td>
      <td valign="top">Basque Red Pearl, Red, Bellanova White Pearl. Most cases Mfg color name is output.</td>
    </tr>
    <tr>
      <td valign="top">Interior Color</td>
      <td valign="top"><code>icolor</code></td>
      <td valign="top">Gasoline, Diesel, Electric Etc.</td>
    </tr>
    <tr>
      <td valign="top">Video URL</td>
      <td valign="top"><code>youtube</code></td>
      <td valign="top">https://www.youtube.com/watch?v=BJt1rdFZXlY</td>
    </tr>
    <tr>
      <td valign="top">Miles</td>
      <td valign="top"><code>miles</code></td>
      <td valign="top">10000, 28000. All non numeric characters will be striped. will be stripped. 10,000 --> 10000</td>
    </tr>
    <tr>
      <td valign="top">Transmission</td>
      <td valign="top"><code>transmission</code></td>
      <td valign="top">8 Speed Automatic</td>
    </tr>
    <tr>
      <td valign="top">Engine</td>
      <td valign="top"><code>engine</code></td>
      <td valign="top">Short Summary of engine | 3.5L V6 (Gasoline) | 5.4L V8 (Diesel)</td>
    </tr>
    <tr>
      <td valign="top">Images Update Timestamp</td>
      <td valign="top"><code>datephotosupdated</code></td>
      <td valign="top">2018-02-04T22:44:30.652Z (ISO 8601 format in UTC)</td>
    </tr>
    <tr>
      <td valign="top">Comments/Description</td>
      <td valign="top"><code>description</code></td>
      <td valign="top">The text description of the vehicle. HTML and Special characters will be removed/replaced and formatted as plain text. The only allowed HTML tag allowed is <br>.</td>
    </tr>
    <tr>
      <td valign="top">Options</td>
      <td valign="top"><code>options</code></td>
      <td valign="top">A separated list of options.  Typically separated with a Comma (,) or PIPE (|).  Power Windows,Power Locks,Power Mirrors,Etc. HTML and Special characters will be removed/replaced and formatted to be compatible with third parties.</td>
    </tr>
    <tr>
      <td valign="top">Conversion Options</td>
      <td valign="top"><code>conversionoptions</code></td>
      <td valign="top">A separated list of conversion options.  Typically separated with a Comma (,) or PIPE (|).  Lowered Floor,Power Ramp,Power Doors,Etc.  HTML and Special characters will be removed/replaced and formatted to be compatible with third parties.</td>
    </tr>
    <tr>
      <td valign="top">Image URLs</td>
      <td valign="top"><code>images</code></td>
      <td valign="top">Comma or Pipe seperated or an Array.<br>Example: https://imgs.dealerexpress.net/picture1.jpg, https://imgs.dealerexpress.net/picture2.jpg, https://imgs.dealerexpress.net/picture3.jpg</td>
    </tr>
    <tr>
      <td valign="top">ConversionID at BLVD.com</td>
      <td valign="top"><code>conversionid</code></td>
      <td valign="top">The Mobility Conversion's ID at BLVD.com. Must be numeric.</td>
    </tr>
    <tr>
      <td valign="top">In Stock Date</td>
      <td valign="top"><code>listdate</code></td>
      <td valign="top">2018-02-04T22:44:30.652Z (ISO 8601 format in UTC)</td>
    </tr>
    <tr>
      <td valign="top">Vehicle Link URL</td>
      <td valign="top"><code>vehicle_link</code></td>
      <td valign="top">URL to vehicle.  IE: http://www.dealerexpress.net/vehicles/2009-dodge-viper</td>
    </tr>
    <tr>
      <td valign="top">Warranty</td>
      <td valign="top"><code>warranty</code></td>
      <td valign="top">Vehicle Warranty</td>
    </tr>
    <tr>
      <td valign="top">Conversion Warranty</td>
      <td valign="top"><code>conversion_warranty</code></td>
      <td valign="top">Warranty on the mobility conversion.</td>
    </tr>
  </tbody>
</table>




