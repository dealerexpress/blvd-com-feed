<img align="right" width="180" src="img/logo.svg"><br>
# BLVD.com Inventory Feed Guidelines
Vehicle inventory feed specifications for sending an automated feed to [BLVD.com](https://www.blvd.com).


## Dealers
In most cases, we already accept a feed from your web provider and configuring a new feed is not necessary. Contact BLVD.com or your web provider to see if an automated feed is already available. If you self host your site you can review the following guidelines to begin setting up a feed.  **If you have a web provider, please share this page with them** so they can begin the setup process.

<br>

## Providers
If your a provider that host multiple dealers, the setup of this feed needs to only happen once. Future dealers can be added to your existing feed using one of the following methods.

- **A Single File:** Add each dealer's inventory to a single file for delivery.
- **File Per Dealer:** For each dealer, a separate file is delivered. If the dealer has multiple locations, you include all locations in that single file.


<br>

<a name="samples"></a>
## Sample Files
Take a look at some samples if you have not created a data feed before.
- [Single Dealer CSV](https://github.com/dealerexpress/dx-blvd-feed-guidelines/blob/master/sample-single-dealer.csv)
- [Multiple Dealer CSV](https://github.com/dealerexpress/dx-blvd-feed-guidelines/blob/master/sample-multiple-dealers.csv)
- [Single Dealer JSON](https://github.com/dealerexpress/dx-blvd-feed-guidelines/blob/master/sample-single-dealer.json)



<br>

<a name="data-types"></a>
### Accepted Data Types
<table>
  <thead>
    <tr>
      <th align="left">Type</th>
      <th align="left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td valign="top"><strong>CSV</strong></td>
      <td valign="top">A standard CSV (Comma Separated Values). With or without a header row is fine, however including a header row is preferred. Column order can be anything you like. CSV data needs to conform to <a href="https://datatracker.ietf.org/doc/html/rfc4180" target="_blank">RFC 4180</a> standards.</td>
    </tr>
    <tr>
          <td valign="top"><strong>JSON</strong></td>
          <td valign="top">We accept data as a JSON Array full of Objects. One object per vehicle. Key names are required to match the specification outlined below in the <a href="#columns">Columns/Fields</a> section. JSON data needs to conform to <a href="https://datatracker.ietf.org/doc/html/rfc4627" target="_blank">RFC 4627</a> standards.</td>
        </tr>
  </tbody>
</table>



<br>

<a name="html"></a>
## HTML
Any HTML found in the data file gets stripped out with the exception of &lt;br&gt; within the description column. Newlines (\n) are converted to &lt;br&gt; within the description field.

<br>

<a name="delivery"></a>
## Delivery Methods
You have the option to either send the file to us or we'll fetch it from your servers.  You may update your feed file as often as you like, however at least once a day is best.
<table>
<thead>
<tr>
<th align="left">Method</th>
     <th align="left">Direction</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
     <td valign="top">FTP</td>
     <td valign="top">Provider Sends</td>
     <td valign="top"><strong>Host: </strong>ftp://api.dealerexpress.net<br><strong>Port: </strong>21<br>Send your file(s) via standard FTP over a non-secure connection.</td>
</tr>
<tr>
     <td valign="top">FTPS</td>
     <td valign="top">Provider Sends</td>
     <td valign="top"><strong>Host: </strong>ftps://api.dealerexpress.net<br><strong>Port: </strong>990<br>Send your file(s) via standard FTP over an implicit SSL/TLS secure connection.</td>
</tr>
     <tr>
     <td valign="top">HTTP/HTTPS</td>
     <td valign="top">BLVD Fetches</td>
     <td valign="top">You may host the file on your servers or in the cloud and we'll retrieve the file from the URL you provide us. You'll need to update the file on your end as inventory changes or at least daily. The URL endpoint must be a publicly available endpoint.</td>
</tr>
</tbody>
</table>

**Note:** After uploading a file via FTP/FTPS our system picks it up shortly after upload is complete and may no longer be visible on the FTP server after being picked up.

<br>

<a name="credentials"></a>
## FTP/FTPS Username & Password
When you are ready to begin sending your feed to BLVD.com, please contact us and we'll provide you with credentials you can use to log on to the FTP/FTPS server.



<br>

<a name="file-naming"></a>
## Naming Your File(s)
You may name your files anything you like as long as they have valid file extensions (.csv or .json). However the name should remain the same with each update. Do not prepend/append your filenames with dates/times.
##### Our Preferred Naming
- **Single Dealer Files:** Name the file {dealerid}.csv or {dealerid}.json
- **Multi Dealer Files:** Name the file blvd.csv or blvd.json


<br>

<a name="images"></a>
## Image URL's
Images should be added via URL's to the publicly available image via HTTP/HTTPS. We'll fetch each image from the URL and host it on BLVD.com for the duration of the vehicle listing. **Vehicles without a dealer loaded image should not include a placeholder**, we'll provide our own placeholder image. Image Types Accepted: **JPG, JPEG, PNG, WEBP**

### Aspect Ratio
Image should ideally be an aspect ratio of 16:9 or 4:3.  Images greater than 4:3 in aspect ratio will be automatically cropped to 4:3 by gravitating toward center.

### Image Size
**Send the largest/best quality image you have.** If you have the original uploaded image available, they work best as each time compression happens the quality is reduced. We'll perform resize and compression to optimize for BLVD.com.

### Ordering Images
Images are ordered on the site as they appear in the feed file. The first image will be the primary image used when customers are browsing vehicle listings.

### Updating An Image
We'll automatically update all the vehicle's images anytime one or more image URL's or the image ordering changes within the feed.



<br>

<a name="required"></a>
## Required Columns/Fields
<table>
<thead>
<tr>
<th align="left">Column/Field</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
     <td valign="top">Dealer ID</td>
     <td valign="top">Vehicles missing this field or containing an invalid Dealer ID will be ignored</td>
</tr>
<tr>
     <td valign="top">VIN</td>
     <td valign="top">Must be a valid 17 digit VIN. VIN's must be unique across the dealer brand. Duplicate VIN's within a dealer will result in the overwriting of prior vehicles with the same VIN. Duplicating vehicles across multiple locations is now allowed.</td>
</tr>
     <tr>
     <td valign="top">Zip Code</td>
     <td valign="top">We use this to match inventory to the correct dealer location. Vehicles with missing or invalid 5 digit zip code will default to the dealer's primary location.</td>
</tr>
</tbody>
</table>


<br>

<a name="file-notes"></a>
## File Notes

<table>
<thead>
<tr>
<th align="left">Type</th>
<th align="left">Notes</th>
</tr>
</thead>
<tbody>
<tr>
     <td valign="top">CSV</td>
     <td valign="top">UTF-8 Encoding. Header Row is Optional. Header row names can be anything, but matching either name or key is preferred. Column order does not matter, however after initialization they should not change.<br><a href="https://github.com/dealerexpress/dx-blvd-feed-guidelines/blob/master/sample-single-dealer.csv" target="_blank">View a sample CSV file</a></td>
</tr>
<tr>
     <td valign="top">JSON</td>
     <td valign="top">UTF-8 Encoding. JSON should be an Array full of Objects IE: [{},{},{}]. Each object represents one vehicle. <strong>Object key names MUST match the key names outlined below.</strong><br><a href="https://github.com/dealerexpress/dx-blvd-feed-guidelines/blob/master/sample-single-dealer.json" target="_blank">View a sample JSON file</a></td>
</tr>
</tbody>
</table>


<br>

<a name="columns"></a>
## Columns/Fields
Here are the columns BLVD.com utilizes. If you already have a feed file template, it should work just fine so long as the required fields are met. Adding additional fields is fine. CSV column order is not important.
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
      <td valign="top">Dealer ID</td>
      <td valign="top"><code>dealerid</code></td>
      <td valign="top">
      <strong style="color: #aa0000">* Required *</strong><br>
      BLVD.com Assigned Dealer ID (Preferred) or Provider's Assigned Dealer ID. <a href="#required">See Requirements</a></td>
    </tr>
    <tr>
      <td valign="top">Zip Code</td>
      <td valign="top"><code>zip</code></td>
      <td valign="top"><strong style="color: #aa0000">* Required *</strong><br>
      Vehicles location 5 digit zip code. <a href="#required">See Requirements</a></td>
    </tr>
    <tr>
      <td valign="top">VIN</td>
      <td valign="top"><code>vin</code></td>
      <td valign="top"><strong style="color: #aa0000">* Required *</strong><br>
      A Valid 17 Digit VIN Number. <a href="#required">See Requirements</a></td>
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
      <td valign="top"><strong>Used Values:</strong> Used, used, USED, U<br>
      <strong>New Values:</strong> New, new, NEW, N<br>
      Defaults to Used
      </td>
    </tr>
    <tr>
      <td valign="top">New/Used (Conversion)</td>
      <td valign="top"><code>conversion_newused</code></td>
      <td valign="top"><strong>Used Values:</strong> Used, used, USED, U<br>
            <strong>New Values:</strong> New, new, NEW, N<br>
            Defaults to "Chassis New/Used"
      </td>
    </tr>
    <tr>
      <td valign="top">Conversion Name</td>
      <td valign="top"><code>conversion</code></td>
      <td valign="top">Vehicle Mobility Conversion Name. A combined conversion manufacturer and model. IE: BraunAbility Entervan XT</td>
    </tr>
    <tr>
      <td valign="top">Stock Number</td>
      <td valign="top"><code>stock</code></td>
      <td valign="top">Examples: 4584B, 45215</td>
    </tr>
    <tr>
      <td valign="top">List Price</td>
      <td valign="top"><code>price</code></td>
      <td valign="top">All non numeric characters will be striped. All characters after a period (.) will be stripped. $19,900.99 --> 19900.<br>Examples: '$19,900', '19900', '28000'</td>
    </tr>
    <tr>
      <td valign="top">Exterior Color</td>
      <td valign="top"><code>e_color</code></td>
      <td valign="top">Examples: Basque Red Pearl, Red, Black</td>
    </tr>
    <tr>
      <td valign="top">Interior Color</td>
      <td valign="top"><code>i_color</code></td>
      <td valign="top">Examples: Tan, Black Leather, Gray</td>
    </tr>
    <tr>
      <td valign="top">Video URL</td>
      <td valign="top"><code>video_url</code></td>
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
      <td valign="top">Comments/Description</td>
      <td valign="top"><code>description</code></td>
      <td valign="top">The text description of the vehicle. HTML and Special characters will be removed/replaced and formatted as plain text. The only allowed HTML tag allowed is &lt;br&gt;.</td>
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
      <td valign="top"><code>images_urls</code></td>
      <td valign="top">Comma or Pipe seperated or an Array.<br>Example: https://imgs.dx.io/img1.jpg, https://imgs.dx.io/img2.jpg, https://imgs.dx.io/img3.jpg</td>
    </tr>
    <tr>
      <td valign="top">ConversionID at BLVD.com</td>
      <td valign="top"><code>conversionid</code></td>
      <td valign="top">The Mobility Conversion's ID at BLVD.com. Must be numeric.</td>
    </tr>
    <tr>
      <td valign="top">In Stock Date</td>
      <td valign="top"><code>listdate</code></td>
      <td valign="top">2018-02-04T22:44:30.652Z (ISO 8601)</td>
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




