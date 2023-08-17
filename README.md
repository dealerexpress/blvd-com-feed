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

<a name="delivery"></a>
## Delivery Methods
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

<br>

<a name="credentials"></a>
## FTP/FTPS Username & Password
When you are ready to begin sending your feed to BLVD.com, please contact us and we'll provide you with credentials you can use to log on to the FTP/FTPS server.

<br>

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
      <td valign="top"><code>conversion_newused</code></td>
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
      <td valign="top"><code>e_color</code></td>
      <td valign="top">Basque Red Pearl, Red, Bellanova White Pearl. Most cases Mfg color name is output.</td>
    </tr>
    <tr>
      <td valign="top">Interior Color</td>
      <td valign="top"><code>i_color</code></td>
      <td valign="top">Gasoline, Diesel, Electric Etc.</td>
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


<br><br>
<a name="contact"></a>
## Contact Information


