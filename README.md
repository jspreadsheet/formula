<h1>JSS Formula Premium</h1>

The JSS Formula Premium is a JavaScript software to parse and execute spreadsheet-like formulas. It handles ranges,
variables, worksheets, and a great number of formulas available in other spreadsheet software such as Excel or
Google Spreadsheet. It deals with the JavaScript precision issues and, it is compatible with Jspreadsheet Pro plugins.<br><br>

This plugin is distributed in two different versions: basic and premium.<br><br>

<table class='table'>
<thead>
<tr>
    <th></th>
    <th style='text-align:center'>Formula Basic</th>
    <th style='text-align:center'>Formula Premium</th>
</tr>
</thead>
<tbody>
<tr><td>License</td><td align='center'>MIT</td><td align='center'>Required a license</td></tr>
<tr><td>Pricing</td><td align='center'>Free</td><td align='center'>180 GBP</td></tr>
<tr><td>Scope</td><td align='center'>window</td><td align='center'>restricted scope</td></tr>
<tr><td>Parser</td><td align='center'>new Function</td><td align='center'>Custom parser</td></tr>
<tr><td>JavaScript precision issues</td><td align='center'>No</td><td align='center'>Yes</td></tr>
<tr><td>Date operations</td><td align='center'>No</td><td align='center'>Yes</td></tr>
<tr><td>Cross worksheets/spreadsheets calculations</td><td align='center'>No</td><td align='center'>Yes *</td></tr>
<tr><td>Defined names</td><td align='center'>No</td><td align='center'>Yes **</td></tr>
<tr><td>Matrix calculations</td><td align='center'>No</td><td align='center'>Yes **</td></tr>
<tr><td>Number of implemented formulas</td><td align='center'>403</td><td align='center'>455</td></tr>
</tbody>
</table>

<br>

<h2>Compatibility</h2>

This software can be used stand-alone or integrated with Jspreadsheet CE, BASE, and PRO.<br><br>

\* Only available on stand-alone and with the PRO distributions.<br>
\*\* Only available on stand-alone and with the PRO v8 distributions.<br>

<br>

<h2>License</h2>

This plugin requires a license that should be associated with one specified domain. If you need a license for
redistribution or SaaS, please keep in touch with contact@jspreadsheet.com<br>

<br>

<h2>Precision</h2>

JSS Formula Premium tackles the JavaScript numeric precision.<br>

<pre class="prettyprint linenums">
// Activate the precision adjust
formula.adjustPrecision = true;

formula('37.02 + 2.56');
// Without adjustPrecision: 39.580000000000005
// With adjustPrecision: 39.58

formula('185.32 - 84.78');
// Without adjustPrecision: 100.53999999999999
// With adjustPrecision: 100.54

formula('25.92 * 3.33');
// Without adjustPrecision: 86.31360000000001
// With adjustPrecision: 86.3136

formula('9.15 / 6');
// Without adjustPrecision: 1.5250000000000001
// With adjustPrecision: 1.525
</pre>

<br>

<p class='small'>NOTE: When this option is enabled, the results will be round in a maximum ten decimal places.</p>

<br>

<h2>Usage</h2>

The formula method receives the expression and the variables that will support the calculations.<br>

<pre class="prettyprint linenums">
@param {string} expression - the formula to be calculated
@param {object} variables - the variables and values necessary to parse the expression
@param {number=} x - a optional coordinate reference
@param {number=} y - a optional coordinate reference

formula(expression: String, variables: Object, [x: Number], [y: Number]) : string|array
</pre>


<br><br>

<h3>Examples</h3>

You can run the following tests on the console of the browser when initiation as above.<br><br>

<h4>Range operations</h4>
<pre class="prettyprint linenums">
formula('A1:B1*2', { A1: 2, B1: 4 });
// Returns Array[ 4, 8 ]

formula('SUM(A1:B1*2)', { A1: 1, B1: 'A2+B2', A2: 3, B2: 4 })
// Returns 16

formula('SUM(A1:A6)', { A1: 2, A2: 4, A3: 5, A4: 1, A5: 5, A6: 1 });
// Returns 18

formula('AVERAGE(CALCULATION*10)', { CALCULATION: 'A1:A3', A1: 1, A2: 2, A3: 3 })
// Returns 20

formula('SUM(B:B)', { B1: 1, B2: 1, B3: 14 });
// Returns 16
</pre>

<h4>Conditional calculations</h4>

<pre class="prettyprint linenums">
formula('IF(B1=0,0,B9/B1)', { B1:0, B9: 3 });
// Returns zero when B1 is zero

formula('IF(true, CALCULATION, 10)', { CALCULATION: 'A1:A3', A1: 1, A2: 2, A3: 3 })
// Returns [[1], [2], [3]]

formula('IF(C16+C15!=0,C13+C14,false)', { C16: 0, C15: 0, C14: 3, C13: 12 })
// Returns false
</pre>

<h4>Comparisions</h4>
<pre class="prettyprint linenums">
formula('1*2<1^4');
// Returns false

formula('(1==1)<>(2>2)')
// Returns true
</pre>

<h4>Date calculations</h4>
<pre class="prettyprint linenums">
formula('NOW()+1');
// Today + one day

formula('DATE(2021,1,1) > DATE(2021,2,1)');
// false
</pre>

<h4>Cross worksheets</h4>
<pre class="prettyprint linenums">
formula('SHEET1!A1*A1', { 'SHEET1!A1': 2, 'A1': 3 });
// Returns 6

formula('SUM(SHEET3!B1:B3)', { 'SHEET3!B1': 3, 'SHEET3!B2': 3, 'SHEET3!B3': 4 });
// Returns 10

formula('SUM(B:B)', { 'B1': 1, 'B2': 2, 'B3': 4 });
// Returns 7
</pre>

<h4>Worksheets operations</h4>
<pre class="prettyprint linenums">
formula('SHEET1!A1*10', { SHEET1: [[1,2,3],[4,5,6]] });
// Returns 1 * 10

formula('SHEET1!B1*SHEET2!B1', { SHEET1: [[1,2,3],[4,5,6]], SHEET2: [[10,20,30]] });
// Returns 2 * 20
</pre>

<br>

<h2>Integrating with Jspreadsheet</h2>

How to integrate Jspreadsheet and the formula-pro plugin.<br><br>

<h3>Using CDN</h3>

<pre class="prettyprint linenums">
&#60;html>
&#60;script src="https://jspreadsheet.com/v8/jspreadsheet.js">&#60;/script>
&#60;script src="https://jsuites.net/v4/jsuites.js">&#60;/script>
&#60;link rel="stylesheet" href="https://jspreadsheet.com/v7/jspreadsheet.css" type="text/css" />
&#60;link rel="stylesheet" href="https://jsuites.net/v4/jsuites.css" type="text/css" />

&#60;script src="https://jspreadsheet.com/v8/plugins/formula-pro.js">&#60;/script>

&lt;div id='spreadsheet'>&lt;/div>

&lt;script>
// License for Formula Plugin
jspreadsheet.license = 'your-license';

// Add-on for Jspreasheet
jspreadsheet.setExtensions({ formula });

// Create the spreadsheets
jspreadsheet(document.getElementById('spreadsheet'), {
    worksheets: [
        { minDimensions: [10, 10] },
        { minDimensions: [10, 10] },
    ],
});
&lt;/script>
&lt;/html>
</pre>

<br>

<h3>Using NPM</h3>

<pre class="prettyprint linenums">
// Jspreadsheet Pro
import jspreadsheet from 'jspreadsheet-pro';

// Formula Premium Plugin
import formula from '@jspreadsheet/formula-pro';

// License for Formula Plugin
jspreadsheet.license = 'your-license';

// Add-on for Jspreasheet
jspreadsheet.setExtensions({ formula });

// Create a spreadsheet
jspreadsheet(document.getElementById('spreadsheet'), {
    worksheets: [
        { minDimensions: [10, 10] },
        { minDimensions: [10, 10] },
    ]
});
</pre>

