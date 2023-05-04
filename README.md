Download Link: https://assignmentchef.com/product/solved-cse-344-homework-7-json-nosql-and-asterixdb
<br>
<strong>Objectives:</strong> To practice writing queries over the semi-structured data model. To be able to manipulate semistructured data in JSON and practice using a NoSQL database system (AsterixDB).




<strong>Resources</strong>

<ul>

 <li><a href="https://github.com/theoliao1998/Data-Management/blob/master/7%20JSON%2C%20NoSQL%2C%20and%20AsterixDB/starter-code">starter code</a>: which contains <code>mondial.adm</code> (the entire dataset), <code>country</code>, <code>mountain</code>, and <code>sea</code> (three subsets)</li>

 <li><a href="https://asterixdb.apache.org/docs/0.9.4/index.html" rel="nofollow">documentation for AsterixDB</a></li>

 <li><a href="https://github.com/theoliao1998/Data-Management/blob/master/7%20JSON%2C%20NoSQL%2C%20and%20AsterixDB/asterix_guide.md">guide written by former TAs</a></li>

</ul>

<h2><a id="user-content-assignment-details" class="anchor" href="https://github.com/theoliao1998/Data-Management/blob/master/7%20JSON%2C%20NoSQL%2C%20and%20AsterixDB/hw7.md#assignment-details" aria-hidden="true"></a>Assignment Details</h2>

In this homework, you will be writing SQL++ queries over the semi-structured data model implemented in <a href="https://asterixdb.apache.org/" rel="nofollow">AsterixDB</a>. Asterix is an Apache project on building a DBMS over data stored in JSON files.

<h3><a id="user-content-mondial-dataset" class="anchor" href="https://github.com/theoliao1998/Data-Management/blob/master/7%20JSON%2C%20NoSQL%2C%20and%20AsterixDB/hw7.md#mondial-dataset" aria-hidden="true"></a>Mondial Dataset</h3>

You will run queries over the <a href="https://www.dbis.informatik.uni-goettingen.de/Mondial/" rel="nofollow">Mondial database</a>, a geographical dataset aggregated from multiple sources. As is common in real-world aggregated data, the Mondial dataset is “messy”; the schema is occassionally inconsistent, and some facts may conflict. We have provided the dataset in ADM format, converted from the XML format available online, for use in AsterixDB.

<h3><a id="user-content-setting-up-asterixdb" class="anchor" href="https://github.com/theoliao1998/Data-Management/blob/master/7%20JSON%2C%20NoSQL%2C%20and%20AsterixDB/hw7.md#setting-up-asterixdb" aria-hidden="true"></a>Setting up AsterixDB</h3>

<ol>

 <li>Download and install AsterixDB. Download the file <a href="https://www.apache.org/dyn/closer.cgi/asterixdb" rel="nofollow"><code>apache-asterixdb-0.9.4.zip</code></a> and unzip it anywhere you’d like.</li>

 <li>Start an instance of AsterixDB using the start-sample-cluster.sh (or .bat if you are on Windows) located in the opt/local/bin folder. <em>Note: AsterixDB requires Java 8; later versions will not work.</em> If you get errors about Java versions, specify a path to Java 8 binaries through a command like: <code>export JAVA_HOME=/usr/lib/jvm/[SOME JAVA 8 folder]</code></li>

 <li>When your AsterixDB instance is running you can enter the query interface by visiting 127.0.0.1:19001 in your favorite web browser.</li>

 <li>Obtain the data for geo from the starter-files directory of your git repository. All of them are JSON data files, you can inspect them using your favorite text editor.</li>

 <li>Create the dataverse of mondial data. Copy and paste the text below in the Query box of the web interface. Edit the <code>&lt;path to mondial.adm&gt;</code>. Then press Run:</li>

 <li>Alternatively, you can use the terminal to run queries rather than the web interface. After you have started Asterix, put your query in a file (say <code>q1.sqlp</code>), then execute the query by typing the following command in terminal:This will print the output on the screen. If there is too much output, you can save it to a fileYou can now view <code>output.txt</code> using your favorite text editor.</li>

 <li>To reference the geo dataverse, use the following statement before each of your queries to declare the geo namespace: <code>USE geo;</code>Try this query to see if things are running correctly:<pre lang="USE"><code>   SELECT y.`-car_code` as code, y.name as name   FROM geo.world x, x.mondial.country y   ORDER BY y.name;</code></pre></li>

 <li>For practice, run, examine, modify these queries. They contain useful templates for the questions on the homework: make sure you understand them.</li>

 <li>To shutdown Asterix, simply run <code>stop-sample-cluster.sh</code> in the terminal. The script is located in <code>opt/local/bin</code> (or <code>optlocalbinstop-sample-cluster.bat</code> on windows).</li>

</ol>

<h3><a id="user-content-problems-100-points" class="anchor" href="https://github.com/theoliao1998/Data-Management/blob/master/7%20JSON%2C%20NoSQL%2C%20and%20AsterixDB/hw7.md#problems-100-points" aria-hidden="true"></a>Problems (100 points)</h3>

<strong>For all questions asking to report free response-type questions, please leave your responses in comments</strong>

Use only the <code>mondial.adm</code> dataset for problems 1-9.

<ol>

 <li>Retrieve all the names of all cities located in Peru, sorted alphabetically. Name your output attribute <code>city</code>. [Result Size: 30 rows of <code>{"city":...}</code>]</li>

 <li>For each country return its name, its population, and the number of religions, sorted alphabetically by country. Report 0 religions for countries without religions. Name your output attributes <code>country</code>, <code>population</code>, <code>num_religions</code>. [Result Size: 238 rows of <code>{"num_religions":..., "country":..., "population":...}</code> (order of keys can differ)]</li>

 <li>For each religion return the number of countries where it occurs; order them in decreasing number of countries. Name your output attributes <code>religion</code>, <code>num_countries</code>. [Result size: 37 of <code>{"religion':..., "num_countries":...}</code> (order of keys can differ)]</li>

 <li>For each ethnic group, return the number of countries where it occurs, as well as the total population world-wide of that group. Hint: you need to multiply the ethnicity’s percentage with the country’s population. Use the functions <code>float(x)</code> and/or <code>int(x)</code> to convert a <code>string</code> to a <code>float</code> or to an <code>int</code>. Name your output attributes <code>ethnic_group</code>, <code>num_countries</code>, <code>total_population</code>. You can leave your final <code>total_population</code> as a <code>float</code> if you like. [Result Size: 262 of <code>{"ethnic_group":..., "num_countries":..., "total_population":...}</code> (order of keys can differ)]</li>

 <li>Compute the list of all mountains, their heights, and the countries where they are located. Here you will join the “mountain” collection with the “country” collection, on the country code. You should return a list consisting of the mountain name, its height, the country code, and country name, in descending order of the height. Name your output attributes <code>mountain</code>, <code>height</code>, <code>country_code</code>, <code>country_name</code>. [Result Size: 272 rows of <code>{"mountain":..., "height":..., "country_code":..., "country_name":...}</code> (order of keys can differ)]Hint: Some mountains can be located in more than one country. You need to output them for each country they are located in.</li>

 <li>Compute a list of countries with all their mountains. This is similar to the previous problem, but now you will group the mountains for each country; return both the mountain name and its height. Your query should return a list where each element consists of the country code, country name, and a list of mountain names and heights; order the countries by the number of mountains they contain, in descending order. Name your output attributes <code>country_code</code>, <code>country_name</code>, <code>mountains</code>. The attribute <code>mountains</code> should be a list of objects, each with the attributes <code>mountain</code> and <code>height</code>. [Result Size: 238 rows of <code>{"country_code":..., "country_name":..., "mountains": [{"mountain":..., "height":...}, {"mountain":..., "height":...}, ...]}</code> (order of keys can differ)]</li>

 <li>Find all countries bordering two or more seas. Here you need to join the “sea” collection with the “country” collection. For each country in your list, return its code, its name, and the list of bordering seas, in decreasing order of the number of seas. Name your output attributes <code>country_code</code>, <code>country_name</code>, <code>seas</code>. The attribute <code>seas</code> should be a list of objects, each with the attribute <code>sea</code>. [Result Size: 74 rows of <code>{"country_code":..., "country_name":..., "seas": [{"sea":...}, {"sea":...}, ...]}</code> (order of keys can differ)]</li>

 <li>Return all landlocked countries. A country is landlocked if it borders no sea. For each country in your list, return its code, its name, in decreasing order of the country’s area. Note: this should be an easy query to derive from the previous one. Name your output attributes <code>country_code</code>, <code>country_name</code>, <code>area</code>. [Result Size: 45 rows of <code>{"country_code":..., "country_name":..., "area":...}</code> (order of keys can differ)]</li>

 <li>For this query you should also measure and report the runtime; it may be approximate (warning: it might run for a while). Find all distinct pairs of countries that share both a mountain and a sea. Your query should return a list of pairs of country names. Avoid including a country with itself, like in (France,France), and avoid listing both (France,Korea) and (Korea,France) (not a real answer). Name your output attributes <code>first_country</code>, <code>second_country</code>. [Result Size: 7 rows of <code>{"first_country":..., "second_country":...}</code>]</li>

</ol>

For problems 10-12 we will ask you to load in the extra datasets provided in starter code.

<ol start="10">

 <li>Create a new dataverse called geoindex, then run the following commands:This created the type <code>countryType</code>, the dataset <code>country</code>, and a <code>BTREE</code> index on the attribute <code>-car_code</code>, which is also the primary key. Both types are OPEN, which means that they may have other fields besides the three required fields <code>-car_code</code>, <code>-area</code>, and population.Create two new types: <code>mountainType</code> and <code>seaType</code>, and two new datasets, <code>mountain</code> and <code>sea</code>. Both should have two required fields: <code>-id</code> and <code>-country</code>. Their key should be autogenerated, and of type <code>uuid</code> (see how we did it for the mondial dataset). Create an index of type <code>KEYWORD</code> (instead of <code>BTREE</code>) on the <code>-country</code> field (for both <code>mountain</code> and <code>sea</code>). Turn in the complete sequence of commands for creating all three types, datasets, and indices (for <code>country</code>, <code>mountain</code>, <code>sea</code>).Recall from lecture that asterix only allows creating index at top level collection, hence we provide the country, sea, etc collections individually even though their data is already included in mondial.</li>

 <li>Re-run the query from 9. (“pairs of countries that share both a mountain and a sea”) on the new dataverse <code>geoindex</code>. Report the new runtime. [Result Size: 7 rows of <code>{"first_country":..., "second_country":...}</code>]</li>

 <li>Modify the query from 11. to return, for each pair of countries, the list of common mountains, and the list of common seas. Name your output attributes <code>first_country</code>, <code>second_country</code>, <code>mountain</code>, <code>sea</code>. [Result Size: 7 rows of <code>{"mountains":[{"mountain":...}, ...], "seas":[{"sea":...}, ...], "first_country":..., "second_country":...}</code>]</li>

</ol>

5/5 - (2 votes)

<pre> DROP DATAVERSE geo IF EXISTS; CREATE DATAVERSE geo;  <span class="pl-k">CREATE</span> <span class="pl-k">TYPE</span> <span class="pl-en">geo</span>.worldType <span class="pl-k">AS</span> {auto_id:uuid }; CREATE DATASET <span class="pl-c1">geo</span>.<span class="pl-c1">world</span>(worldType)  <span class="pl-k">PRIMARY KEY</span> auto_id AUTOGENERATED; LOAD DATASET <span class="pl-c1">geo</span>.<span class="pl-c1">world</span> USING localfs         ((<span class="pl-s"><span class="pl-pds">"</span>path<span class="pl-pds">"</span></span><span class="pl-k">=</span><span class="pl-s"><span class="pl-pds">"</span>127.0.0.1:///&lt;path to mondial.adm&gt;, e.g., /home/auser/344/hw/geo/mondial.adm<span class="pl-pds">"</span></span>),(<span class="pl-s"><span class="pl-pds">"</span>format<span class="pl-pds">"</span></span><span class="pl-k">=</span><span class="pl-s"><span class="pl-pds">"</span>adm<span class="pl-pds">"</span></span>)); <span class="pl-c">/* Edit the absolute path above to point to your copy of mondial.adm. */</span> <span class="pl-c">/* Use '/' instead of '' in a path for Windows. e.g., C:/344/hw/geo/mondial.adm. */</span></pre>

<pre>curl -v --data-urlencode <span class="pl-s"><span class="pl-pds">"</span>statement=<span class="pl-pds">`</span>cat q1.sqlp<span class="pl-pds">`</span><span class="pl-pds">"</span></span> --data pretty=true http://localhost:19002/query/service</pre>

<pre>curl -v --data-urlencode <span class="pl-s"><span class="pl-pds">"</span>statement=<span class="pl-pds">`</span>cat q1.sqlp<span class="pl-pds">`</span><span class="pl-pds">"</span></span> --data pretty=true http://localhost:19002/query/service  <span class="pl-k">&gt;</span>  output.txt</pre>

<pre><span class="pl-c">-- return the set of countries</span><span class="pl-k">SELECT</span> <span class="pl-c1">x</span>.<span class="pl-c1">mondial</span>.country <span class="pl-k">FROM</span> <span class="pl-c1">geo</span>.<span class="pl-c1">world</span> x;</pre>

<pre><span class="pl-c">-- return each country, one by one (see the difference?)</span><span class="pl-k">SELECT</span> y <span class="pl-k">as</span> country <span class="pl-k">FROM</span> <span class="pl-c1">geo</span>.<span class="pl-c1">world</span> x, <span class="pl-c1">x</span>.<span class="pl-c1">mondial</span>.country y;</pre>

<pre><span class="pl-c">-- return just their codes, and their names, alphabetically</span><span class="pl-c">-- notice that -car_code is not a legal field name, so we enclose in ` … `</span><span class="pl-k">SELECT</span> y.<span class="pl-s"><span class="pl-pds">`</span>-car_code<span class="pl-pds">`</span></span> <span class="pl-k">as</span> code, <span class="pl-c1">y</span>.<span class="pl-c1">name</span> <span class="pl-k">as</span> name<span class="pl-k">FROM</span> <span class="pl-c1">geo</span>.<span class="pl-c1">world</span> x, <span class="pl-c1">x</span>.<span class="pl-c1">mondial</span>.country y <span class="pl-k">order by</span> <span class="pl-c1">y</span>.<span class="pl-c1">name</span>;</pre>

<pre><span class="pl-c">-- this query will NOT run...</span><span class="pl-k">SELECT</span> <span class="pl-c1">z</span>.<span class="pl-c1">name</span> <span class="pl-k">as</span> province_name, <span class="pl-c1">u</span>.<span class="pl-c1">name</span> <span class="pl-k">as</span> city_name<span class="pl-k">FROM</span> <span class="pl-c1">geo</span>.<span class="pl-c1">world</span> x, <span class="pl-c1">x</span>.<span class="pl-c1">mondial</span>.country y, <span class="pl-c1">y</span>.<span class="pl-c1">province</span> z, <span class="pl-c1">z</span>.<span class="pl-c1">city</span> u<span class="pl-k">WHERE</span>  <span class="pl-c1">y</span>.<span class="pl-c1">name</span><span class="pl-k">=</span><span class="pl-s"><span class="pl-pds">'</span>Hungary<span class="pl-pds">'</span></span>;<span class="pl-c">-- ...because some provinces have a single city, others have a list of cities; fix it:</span><span class="pl-k">SELECT</span> <span class="pl-c1">z</span>.<span class="pl-c1">name</span> <span class="pl-k">as</span> province_name, <span class="pl-c1">u</span>.<span class="pl-c1">name</span> <span class="pl-k">as</span> city_name<span class="pl-k">FROM</span> <span class="pl-c1">geo</span>.<span class="pl-c1">world</span> x, <span class="pl-c1">x</span>.<span class="pl-c1">mondial</span>.country y, <span class="pl-c1">y</span>.<span class="pl-c1">province</span> z,             CASE  WHEN is_array(<span class="pl-c1">z</span>.<span class="pl-c1">city</span>) THEN <span class="pl-c1">z</span>.<span class="pl-c1">city</span>                  ELSE [<span class="pl-c1">z</span>.<span class="pl-c1">city</span>] END u<span class="pl-k">WHERE</span>  <span class="pl-c1">y</span>.<span class="pl-c1">name</span><span class="pl-k">=</span><span class="pl-s"><span class="pl-pds">'</span>Hungary<span class="pl-pds">'</span></span>;</pre>

<pre><span class="pl-c">-- same, but return the city names as a nested collection; </span><span class="pl-c">-- note correct treatment of missing cities</span><span class="pl-c">-- also note the convenient LET construct (see SQL++ documentation)</span><span class="pl-k">SELECT</span> <span class="pl-c1">z</span>.<span class="pl-c1">name</span> <span class="pl-k">as</span> province_name, (<span class="pl-k">select</span> <span class="pl-c1">u</span>.<span class="pl-c1">name</span> <span class="pl-k">from</span> cities u)<span class="pl-k">FROM</span> <span class="pl-c1">geo</span>.<span class="pl-c1">world</span> x, <span class="pl-c1">x</span>.<span class="pl-c1">mondial</span>.country y, <span class="pl-c1">y</span>.<span class="pl-c1">province</span> zLET cities <span class="pl-k">=</span> CASE  WHEN <span class="pl-c1">z</span>.<span class="pl-c1">city</span> is missing THEN []                   WHEN is_array(<span class="pl-c1">z</span>.<span class="pl-c1">city</span>) THEN <span class="pl-c1">z</span>.<span class="pl-c1">city</span>                   ELSE [<span class="pl-c1">z</span>.<span class="pl-c1">city</span>] END<span class="pl-k">WHERE</span>  <span class="pl-c1">y</span>.<span class="pl-c1">name</span><span class="pl-k">=</span><span class="pl-s"><span class="pl-pds">'</span>Hungary<span class="pl-pds">'</span></span>;</pre>