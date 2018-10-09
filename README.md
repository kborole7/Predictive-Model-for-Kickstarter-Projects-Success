#  Web Scraping Yelp, Text Mining, and Sentiment Analysis of Restaurant Reviews


To Read Full blog open link:

https://medium.com/@kborole7/web-scraping-yelp-text-mining-and-sentiment-analysis-for-restaurant-reviews-ea500e1ef84d


<!DOCTYPE html><html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8"><title>Web Scraping Yelp, Text Mining and Sentiment Analysis for Restaurant Reviews</title><style>
      * {
        font-family: Georgia, Cambria, "Times New Roman", Times, serif;
      }
      html, body {
        margin: 0;
        padding: 0;
      }
      h1 {
        font-size: 50px;
        margin-bottom: 17px;
        color: #333;
      }
      h2 {
        font-size: 24px;
        line-height: 1.6;
        margin: 30px 0 0 0;
        margin-bottom: 18px;
        margin-top: 33px;
        color: #333;
      }
      h3 {
        font-size: 30px;
        margin: 10px 0 20px 0;
        color: #333;
      }
      header {
        width: 640px;
        margin: auto;
      }
      section {
        width: 640px;
        margin: auto;
      }
      section p {
        margin-bottom: 27px;
        font-size: 20px;
        line-height: 1.6;
        color: #333;
      }
      section img {
        max-width: 640px;
      }
      footer {
        padding: 0 20px;
        margin: 50px 0;
        text-align: center;
        font-size: 12px;
      }
      .aspectRatioPlaceholder {
        max-width: auto !important;
        max-height: auto !important;
      }
      .aspectRatioPlaceholder-fill {
        padding-bottom: 0 !important;
      }
      header,
      section[data-field=subtitle] {
        display: none;
      }
      </style></head><body><article class="h-entry">
<header>
<h1 class="p-name">Web Scraping Yelp, Text Mining and Sentiment Analysis for Restaurant Reviews</h1>
</header>
<section data-field="subtitle" class="p-summary">
Yelp is a local search search service for local businesses. People share their reviews about their experience with that business, which is…
</section>
<section data-field="body" class="e-content">
<section name="64ba" class="section section--body section--first section--last"><div class="section-divider"><hr class="section-divider"></div><div class="section-content"><div class="section-inner sectionLayout--insetColumn"><h3 name="bdde" id="bdde" class="graf graf--h3 graf--leading graf--title">Web Scraping Yelp, Text Mining and Sentiment Analysis for Restaurant Reviews</h3><figure name="62eb" id="62eb" class="graf graf--figure graf-after--h3"><div class="aspectRatioPlaceholder is-locked" style="max-width: 456px; max-height: 286px;"><div class="aspectRatioPlaceholder-fill" style="padding-bottom: 62.7%;"></div><img class="graf-image" data-image-id="1*EW7vUH4XLCSIiWAmJLvV8g.jpeg" data-width="456" data-height="286" data-is-featured="true" src="https://cdn-images-1.medium.com/max/800/1*EW7vUH4XLCSIiWAmJLvV8g.jpeg"></div></figure><p name="8764" id="8764" class="graf graf--p graf-after--figure">Yelp is a local search search service for local businesses. People share their reviews about their experience with that business, which is a very crucial source of information. Customer’s feedback can help identify and prioritize strengths and weaknesses for further development of the business. I am interested in the customer reviews for restaurants near me, location Chicago, IL.</p><p name="ee3b" id="ee3b" class="graf graf--p graf-after--p">Thanks to internet, today we have an access to numerous sources where people willingly share their experience with different companies and services. We can use this opportunity to extract some valuable information and derive some actionable-insights to deliver best customer experience.</p><p name="1029" id="1029" class="graf graf--p graf-after--p">By scraping all those reviews we can collect a decent amount of quantitative and qualitative data, analyze it, and identify areas for improvement. Thankfully, python provides libraries to easily deal with these tasks. For web scraping I decided to use requests library, which does the job and is very simple to use. I have no prior experience in web scraping and I want to create my own data set to perform sentiment analysis.</p><p name="54d7" id="54d7" class="graf graf--p graf-after--p">We can easily study the structure of the website by inspecting the website in a web browser. After studying the structure of <a href="https://www.yelp.com/" data-href="https://www.yelp.com/" class="markup--anchor markup--p-anchor" rel="noopener" target="_blank">Yelp web-site</a>, I came up with a list of possible data variables to collect:</p><ol class="postList"><li name="533a" id="533a" class="graf graf--li graf-after--p">Reviewer’s Name</li><li name="3398" id="3398" class="graf graf--li graf-after--li">Review</li><li name="cefe" id="cefe" class="graf graf--li graf-after--li">Date</li><li name="99b5" id="99b5" class="graf graf--li graf-after--li">Star Rating</li><li name="3755" id="3755" class="graf graf--li graf-after--li">Restaurant Name</li></ol><p name="0441" id="0441" class="graf graf--p graf-after--li">The requests module lets you easily download files from the web. You can install the requests module using:</p><p name="9b33" id="9b33" class="graf graf--p graf-after--p"><code class="markup--code markup--p-code">&gt;&gt;&gt; pip install requests</code></p><p name="3404" id="3404" class="graf graf--p graf-after--p">First, we go to the yelp website and search restaurants near me, location Chicago, IL.</p><p name="095b" id="095b" class="graf graf--p graf-after--p">Then, we will import all required libraries and create a pandas DataFrame.</p><pre name="88e1" id="88e1" class="graf graf--pre graf-after--p">import pandas as pd <br>import time as t<br>from lxml import html <br>import requests</pre><pre name="7c0f" id="7c0f" class="graf graf--pre graf-after--pre">reviews_df=pd.DataFrame()</pre><p name="04ff" id="04ff" class="graf graf--p graf-after--pre">Downloading the html page with requests.get()</p><p name="5914" id="5914" class="graf graf--p graf-after--p"><code class="markup--code markup--p-code">&gt;&gt;&gt;import requests</code></p><p name="6f8c" id="6f8c" class="graf graf--p graf-after--p"><code class="markup--code markup--p-code">&gt;&gt;&gt; searchlink= &#39;https://www.yelp.com/search?find_desc=Restaurants&amp;find_loc=Chicago,+IL&#39;</code></p><pre name="338f" id="338f" class="graf graf--pre graf-after--p">user_agent = ‘ Enter you user agent here ’<br>headers = {‘User-Agent’: user_agent}<br><br></pre><p name="f72f" id="f72f" class="graf graf--p graf-after--pre">You can get your user agent <a href="http://www.whatsmyua.info/" data-href="http://www.whatsmyua.info/" class="markup--anchor markup--p-anchor" rel="noopener" target="_blank">here</a>.</p><p name="e84f" id="e84f" class="graf graf--p graf-after--p">You can simply copy paste the url to scrape restaurants reviews for any other location on the same review platform. All you need to do is to specify a link.</p><pre name="1889" id="1889" class="graf graf--pre graf-after--p">page = requests.get(searchlink, headers = headers)<br>parser = html.fromstring(page.content)</pre><p name="af64" id="af64" class="graf graf--p graf-after--pre">The requests.get will download the html page. Now, we have to find the links for multiple restaurants from the page.</p><pre name="90d0" id="90d0" class="graf graf--pre graf-after--p">businesslink=parser.xpath(&#39;//a[<a href="http://twitter.com/class" data-href="http://twitter.com/class" class="markup--anchor markup--pre-anchor" title="Twitter profile for @class" rel="noopener" target="_blank">@class</a>=&quot;biz-name js-analytics-click&quot;]&#39;)<br>links = [l.get(&#39;href&#39;) for l in businesslink]</pre><p name="9e32" id="9e32" class="graf graf--p graf-after--pre">These links are not complete, and therefore we will have to add domain name to it.</p><pre name="5b9a" id="5b9a" class="graf graf--pre graf-after--p">u=[]<br>for link in links:<br>        <br>        u.append(&#39;<a href="https://www.yelp.com%27+" data-href="https://www.yelp.com&#39;+" class="markup--anchor markup--pre-anchor" rel="nofollow noopener" target="_blank">https://www.yelp.com&#39;+</a> str(link))</pre><p name="ec55" id="ec55" class="graf graf--p graf-after--pre">Now we have all the restaurant names from the first page; there are 30 search results in each page. Now lets iterate through each page and get their reviews.</p><pre name="aa57" id="aa57" class="graf graf--pre graf-after--p">for item in u:<br>    page = requests.get(item, headers = headers)<br>    parser = html.fromstring(page.content)</pre><p name="be6a" id="be6a" class="graf graf--p graf-after--pre">The reviews are contained in a div with class name “review review — with-sidebar”. Lets grab all these divs.</p><pre name="b09b" id="b09b" class="graf graf--pre graf-after--p">xpath_reviews = ‘//div[<a href="http://twitter.com/class" data-href="http://twitter.com/class" class="markup--anchor markup--pre-anchor" title="Twitter profile for @class" rel="noopener" target="_blank">@class</a>=”review review — with-sidebar”]’<br>reviews = parser.xpath(xpath_reviews)</pre><p name="f018" id="f018" class="graf graf--p graf-after--pre">For each review we want to scrape the author name, review body, date, restaurant name, and star rating.</p><pre name="b2b3" id="b2b3" class="graf graf--pre graf-after--p">for review in reviews:<br>            <br>       temp = review.xpath(&#39;.//div[contains(<a href="http://twitter.com/class" data-href="http://twitter.com/class" class="markup--anchor markup--pre-anchor" title="Twitter profile for @class" rel="noopener" target="_blank">@class</a>, &quot;i-stars i-                                                stars--regular&quot;)]&#39;)<br>      <br>       rating = [td.get(&#39;title&#39;) for td in temp]</pre><pre name="0f96" id="0f96" class="graf graf--pre graf-after--pre">       xpath_author  = &#39;.//a[<a href="http://twitter.com/id" data-href="http://twitter.com/id" class="markup--anchor markup--pre-anchor" title="Twitter profile for @id" rel="noopener" target="_blank">@id</a>=&quot;dropdown_user-name&quot;]//text()&#39;<br>       xpath_body    = &#39;.//p[<a href="http://twitter.com/lang" data-href="http://twitter.com/lang" class="markup--anchor markup--pre-anchor" title="Twitter profile for @lang" rel="noopener" target="_blank">@lang</a>=&quot;en&quot;]//text()&#39;<br>    <br>       author  = review.xpath(xpath_author)<br>    <br>       date    = review.xpath(&#39;.//span[<a href="http://twitter.com/class" data-href="http://twitter.com/class" class="markup--anchor markup--pre-anchor" title="Twitter profile for @class" rel="noopener" target="_blank">@class</a>=&quot;rating-qualifier&quot;]//text()&#39;)<br>    <br>       body    = review.xpath(xpath_body)<br>        <br>       heading= parser.xpath(&#39;//h1[contains(<a href="http://twitter.com/class" data-href="http://twitter.com/class" class="markup--anchor markup--pre-anchor" title="Twitter profile for @class" rel="noopener" target="_blank">@class</a>,&quot;biz-page-title embossed-text-white&quot;)]&#39;)<br>       bzheading = [td.text for td in heading]</pre><p name="2566" id="2566" class="graf graf--p graf-after--pre">We will create a dictionary for all these items and then we will add this dictionary in a pandas data frame.</p><pre name="23c1" id="23c1" class="graf graf--pre graf-after--p">review_dict = {‘restaurant’ : bzheading,<br>                ‘rating’: rating, <br>                ‘author’: author, <br>                ‘date’: date,<br>                ‘Review’: body,<br>              }<br> reviews_df = reviews_df.append(review_dict, ignore_index=True)</pre><p name="132a" id="132a" class="graf graf--p graf-after--pre">Now we have all the reviews from one page. You can iterate through the pages by finding the maximum page number. The last page number is contained in a &lt;a&gt; tag with class name “available-number pagination-links_anchor”.</p><pre name="44a9" id="44a9" class="graf graf--pre graf-after--p">page_nums = &#39;//a[<a href="http://twitter.com/class" data-href="http://twitter.com/class" class="markup--anchor markup--pre-anchor" title="Twitter profile for @class" rel="noopener" target="_blank">@class</a>=&quot;available-number pagination-links_anchor&quot;]&#39;<br>pg = parser.xpath(page_nums)</pre><pre name="8a4f" id="8a4f" class="graf graf--pre graf-after--pre">max_pg=len(pg)+1</pre><p name="48d5" id="48d5" class="graf graf--p graf-after--pre">Remember to add sleep time inside each for loop to make the script slow and respect the scraping policies of yelp.com. Sending too many requests can get your IP blocked.</p><pre name="cc8d" id="cc8d" class="graf graf--pre graf-after--p">import time as t<br>t.sleep(10)   </pre><p name="77d5" id="77d5" class="graf graf--p graf-after--pre">With the above script, I have scraped a total of 23,869 reviews, for 450 restaurants and 20–60 reviews per restaurant.</p><p name="da8c" id="da8c" class="graf graf--p graf-after--p">Now lets open up a jupyter notebook and perform text mining and sentiment analysis.</p><p name="3a8e" id="3a8e" class="graf graf--p graf-after--p">First import some necessary libraries.</p><pre name="3c52" id="3c52" class="graf graf--pre graf-after--p">import pandas as pd<br>import numpy as np<br>import matplotlib.pyplot as plt<br>import seaborn as sns</pre><p name="0937" id="0937" class="graf graf--p graf-after--pre">I have saved the data in a file named all.csv</p><pre name="b3e8" id="b3e8" class="graf graf--pre graf-after--p">data=pd.read_csv(‘all.csv’)</pre><p name="d3e7" id="d3e7" class="graf graf--p graf-after--pre">Now lets look at the head and tail of the data frame.</p><figure name="3b67" id="3b67" class="graf graf--figure graf-after--p"><div class="aspectRatioPlaceholder is-locked" style="max-width: 700px; max-height: 414px;"><div class="aspectRatioPlaceholder-fill" style="padding-bottom: 59.099999999999994%;"></div><img class="graf-image" data-image-id="1*0mNEovhmt5np_XXKEdqw1A.png" data-width="937" data-height="554" src="https://cdn-images-1.medium.com/max/800/1*0mNEovhmt5np_XXKEdqw1A.png"></div></figure><p name="4a88" id="4a88" class="graf graf--p graf-after--figure">We have 23,869 records with 5 columns. As we can see the data needs formatting. All the unnecessary symbols, tags, and spaces should be removed. There are also some Null/NaN values.</p><p name="5c3b" id="5c3b" class="graf graf--p graf-after--p">Drop all Null/NaN values from the data frame.</p><pre name="a05c" id="a05c" class="graf graf--pre graf-after--p">data.dropna()</pre><p name="d64c" id="d64c" class="graf graf--p graf-after--pre">Now using string slicing, we will remove the unnecessary symbols and spaces.</p><pre name="41f3" id="41f3" class="graf graf--pre graf-after--p">data[&#39;Review&#39;]=data.Review.str[2:-2]<br>data[&#39;author&#39;]=data.author.str[2:-2]<br>data[&#39;date&#39;]=data.date.str[12:-8]<br>data[&#39;rating&#39;]=data.rating.str[2:-2]<br>data[&#39;restaurant&#39;]=data.restaurant.str[16:-12]<br>data[&#39;rating&#39;]=data.rating.str[:1]</pre><figure name="db1c" id="db1c" class="graf graf--figure graf-after--pre"><div class="aspectRatioPlaceholder is-locked" style="max-width: 700px; max-height: 271px;"><div class="aspectRatioPlaceholder-fill" style="padding-bottom: 38.7%;"></div><img class="graf-image" data-image-id="1*--BEZgSNxuvybnn2Xo2Oug.png" data-width="728" data-height="282" src="https://cdn-images-1.medium.com/max/800/1*--BEZgSNxuvybnn2Xo2Oug.png"></div></figure><p name="b0b3" id="b0b3" class="graf graf--p graf-after--figure">Now lets explore the data further.</p><figure name="50b1" id="50b1" class="graf graf--figure graf-after--p"><div class="aspectRatioPlaceholder is-locked" style="max-width: 700px; max-height: 264px;"><div class="aspectRatioPlaceholder-fill" style="padding-bottom: 37.7%;"></div><img class="graf-image" data-image-id="1*vyMRgu1Y0nmRxgXRPxG-YA.png" data-width="1273" data-height="480" src="https://cdn-images-1.medium.com/max/800/1*vyMRgu1Y0nmRxgXRPxG-YA.png"></div></figure><p name="d090" id="d090" class="graf graf--p graf-after--figure">We have maximum number of reviews with a 5 star rating with a total of 11,859 records and the lowest is 979 records for 1 star rating. But there are also some records with an unknown rating ‘t’. These records should be dropped.</p><pre name="56e4" id="56e4" class="graf graf--pre graf-after--p">data.drop(data[data.rating==&#39;t&#39;].index , inplace =True)</pre><p name="5f68" id="5f68" class="graf graf--p graf-after--pre">To understand the data more we can create a new feature call review_length. This column will store the number of characters in each review and we will eliminate any white spaces in the review.</p><pre name="a6cf" id="a6cf" class="graf graf--pre graf-after--p">data[&#39;review_length&#39;] = data[&#39;Review&#39;].apply(lambda x: len(x) - x.count(&#39; &#39;))</pre><p name="79cf" id="79cf" class="graf graf--p graf-after--pre">Now lets plot some graphs and understand the data.</p><pre name="025d" id="025d" class="graf graf--pre graf-after--p">hist = sns.FacetGrid(data=data, col=&#39;rating&#39;)<br>hist.map(plt.hist, &#39;review_length&#39;, bins=50)</pre></div><div class="section-inner sectionLayout--outsetColumn"><figure name="8930" id="8930" class="graf graf--figure graf--layoutOutsetCenter graf-after--pre"><div class="aspectRatioPlaceholder is-locked" style="max-width: 1000px; max-height: 234px;"><div class="aspectRatioPlaceholder-fill" style="padding-bottom: 23.400000000000002%;"></div><img class="graf-image" data-image-id="1*_1wxOO7pFrfK1KY6ARIBdQ.png" data-width="1369" data-height="321" src="https://cdn-images-1.medium.com/max/1000/1*_1wxOO7pFrfK1KY6ARIBdQ.png"></div><figcaption class="imageCaption">Histograms for each star rating and their review length distribution</figcaption></figure></div><div class="section-inner sectionLayout--insetColumn"><p name="e356" id="e356" class="graf graf--p graf-after--figure">We see that there are higher number of 4 and 5 star reviews. The distribution of review lengths are very similar for all ratings.</p><p name="6c38" id="6c38" class="graf graf--p graf-after--p">Now lets create a box plot for the same.</p><pre name="2d3b" id="2d3b" class="graf graf--pre graf-after--p">sns.boxplot(x=&#39;rating&#39;, y=&#39;review_length&#39;, data=data)</pre><figure name="3b70" id="3b70" class="graf graf--figure graf-after--pre"><div class="aspectRatioPlaceholder is-locked" style="max-width: 700px; max-height: 425px;"><div class="aspectRatioPlaceholder-fill" style="padding-bottom: 60.8%;"></div><img class="graf-image" data-image-id="1*f7F1iJhk7WdtNk4cDN_qiQ.png" data-width="752" data-height="457" src="https://cdn-images-1.medium.com/max/800/1*f7F1iJhk7WdtNk4cDN_qiQ.png"></div><figcaption class="imageCaption">Box plot for rating vs review length</figcaption></figure><p name="0882" id="0882" class="graf graf--p graf-after--figure">From the box plot it looks like the 2 and 3 star ratings have higher review lengths than the reviews having 5 star rating. But there are many outliers for each star rating which is evident by the number of dots above the boxes. So the review length wont be a much useful feature for our sentiment analysis.</p><h3 name="c5e7" id="c5e7" class="graf graf--h3 graf-after--p">Sentiment Analysis</h3><p name="e250" id="e250" class="graf graf--p graf-after--h3">In order to determine whether a review is positive or negative we will focus only on the 1 star and 5 star ratings. Lets create a new data frame to store the 1 and 5 star ratings.</p><pre name="59f2" id="59f2" class="graf graf--pre graf-after--p">df = data[(data[&#39;rating&#39;] == 1) | (data[&#39;rating&#39;] == 5)]<br>df.shape</pre><pre name="fa22" id="fa22" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">Output</strong>:(12838, 6)</pre><p name="402b" id="402b" class="graf graf--p graf-after--pre">Out of 23,869 records we now have 12,838 records for 1 and 5 star ratings.</p><p name="7a3a" id="7a3a" class="graf graf--p graf-after--p">In order to use these reviews for analysis, the review text must be formatted properly. Lets check with a sample to understand what we are dealing with.</p></div><div class="section-inner sectionLayout--outsetColumn"><figure name="db75" id="db75" class="graf graf--figure graf--layoutOutsetCenter graf-after--p"><div class="aspectRatioPlaceholder is-locked" style="max-width: 1000px; max-height: 316px;"><div class="aspectRatioPlaceholder-fill" style="padding-bottom: 31.6%;"></div><img class="graf-image" data-image-id="1*gxhQdjBR_kCz6LQGW6lSPg.png" data-width="1521" data-height="481" src="https://cdn-images-1.medium.com/max/1000/1*gxhQdjBR_kCz6LQGW6lSPg.png"></div><figcaption class="imageCaption">First review from the data frame</figcaption></figure></div><div class="section-inner sectionLayout--insetColumn"><p name="25d3" id="25d3" class="graf graf--p graf-after--figure">Looks like there are a lot of punctuation symbols and some unknown codes like ‘\xa0’. ‘\xao’ is actually non-breaking space in Latin1 (ISO 8859–1), also chr(160). You should replace it with a space. Now lets create a function to remove all the punctuation, stop words and then perform lemmatization of the text.</p><p name="9df0" id="9df0" class="graf graf--p graf-after--p">A common method for text pre-processing in natural language processing is bag of words. Bag-of-words represents a list of words disregarding the grammar and their order. The bag-of-words model is commonly used where the occurrence of each word is used as a feature for training a classifier.</p><p name="12a8" id="12a8" class="graf graf--p graf-after--p"><strong class="markup--strong markup--p-strong">Lemmatization</strong>: Lemmatization is a process of grouping together the inflected forms of words so they can be analyzed as a single term, identified as lemma. Lemmatization will always return a dictionary form of a word. For example, the words: type, typed and typing will be considered as one word ‘type’. This feature will be very useful for our analysis.</p><pre name="b046" id="b046" class="graf graf--pre graf-after--p">import string     # Imports the library<br>import nltk        # Imports the natural language toolkit<br>nltk.download(&#39;stopwords&#39;)   # Download the stopwords dataset<br>nltk.download(&#39;wordnet&#39;)<br>wn=nltk.WordNetLemmatizer()</pre><pre name="1e7b" id="1e7b" class="graf graf--pre graf-after--pre">from nltk.corpus import stopwords<br>stopwords.words(&#39;english&#39;)[0:10]</pre><pre name="5bc6" id="5bc6" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">Output:</strong> [&#39;i&#39;, &#39;me&#39;, &#39;my&#39;, &#39;myself&#39;, &#39;we&#39;, &#39;our&#39;, &#39;ours&#39;, &#39;ourselves&#39;, &#39;you&#39;, &quot;you&#39;re&quot;]</pre><p name="aef1" id="aef1" class="graf graf--p graf-after--pre">These stop words are often repeated and are neutral in nature. They don’t represent any positive or negative value and can be ignored.</p><pre name="5406" id="5406" class="graf graf--pre graf-after--p">def text_process_lemmatize(revw):<br>    &quot;&quot;&quot;<br>    Takes in a string of text, then performs the following:<br>    1. Remove all punctuation<br>    2. Remove all stopwords<br>    3. create a list of the cleaned text<br>    4. Return Lemmatize version of the list<br>    &quot;&quot;&quot;<br>    <br>    # Replace the xa0 with a space<br>    revw=revw.replace(&#39;xa0&#39;,&#39; &#39;)<br>    <br>    # Check characters to see if they are in punctuation<br>    nopunc = [char for char in revw if char not in string.punctuation]</pre><pre name="0497" id="0497" class="graf graf--pre graf-after--pre">    # Join the characters again to form the string.<br>    nopunc = &#39;&#39;.join(nopunc)<br>    <br>    # Now just remove any stopwords<br>    token_text= [word for word in nopunc.split() if word.lower() not in stopwords.words(&#39;english&#39;)]<br>    <br>    # perform lemmatization of the above list<br>    cleantext= &#39; &#39;.join(wn.lemmatize(word) for word in token_text)<br>        <br>    return cleantext</pre><p name="f048" id="f048" class="graf graf--p graf-after--pre">Now lets process our review column into the function we just created.</p><pre name="8a82" id="8a82" class="graf graf--pre graf-after--p">df[&#39;LemmText&#39;]=df[&#39;Review&#39;].apply(text_process_lemmatize)</pre><h4 name="eb4f" id="eb4f" class="graf graf--h4 graf-after--pre">Vectorisation</h4><p name="318b" id="318b" class="graf graf--p graf-after--h4">We need to convert the list of lemmas in df[‘LemmText’] into vectors so that a machine learning algorithm and python can use and understand it. This process is know as Vectorizing. This process will create a matrix with each review as a row and each unique lemma as a column and will contain the number of occurrences of each lemma. We will use Count Vectorizer and N-grams process from the scikit-learn library. In that we will focus only on unigrams.</p><pre name="5549" id="5549" class="graf graf--pre graf-after--p">from sklearn.feature_extraction.text import CountVectorizer<br>ngram_vect = CountVectorizer(ngram_range=(1,1))<br>X_counts = ngram_vect.fit_transform(df[&#39;LemmText&#39;])</pre><h4 name="9104" id="9104" class="graf graf--h4 graf-after--pre">Train Test Split</h4><p name="a57f" id="a57f" class="graf graf--p graf-after--h4">Now lets create training and testing data sets using train_test_split from scikit-learn.</p><pre name="7b17" id="7b17" class="graf graf--pre graf-after--p">X_train, X_test, y_train, y_test = train_test_split(X, y,test_size=0.3)</pre><pre name="f72e" id="f72e" class="graf graf--pre graf-after--pre">#0.3 mean the training set will be 70% and test set will be 30%</pre><p name="5571" id="5571" class="graf graf--p graf-after--pre">We will use the Multinomial Naive Bayes for predicting the sentiment. 1 star ratings represent negative reviews and 5 star ratings represent positive reviews. Lets create a MultinomialNB model to fit with X_train and y_train.</p><pre name="7f5d" id="7f5d" class="graf graf--pre graf-after--p">from sklearn.naive_bayes import MultinomialNB<br>nb = MultinomialNB()<br>nb.fit(X_train,y_train)</pre><p name="988b" id="988b" class="graf graf--p graf-after--pre">Now lets predict on the test set X_test.</p><pre name="b698" id="b698" class="graf graf--pre graf-after--p">NBpredictions = nb.predict(X_test)</pre><h4 name="1a98" id="1a98" class="graf graf--h4 graf-after--pre">Evaluation</h4><p name="9c08" id="9c08" class="graf graf--p graf-after--h4">Now lets evaluate our model’s prediction against their actual star ratings from y_test.</p><pre name="ec6a" id="ec6a" class="graf graf--pre graf-after--p">from sklearn.metrics import confusion_matrix,classification_report<br>print(confusion_matrix(y_test,NBpredictions))<br>print(&#39;\n&#39;)<br>print(classification_report(y_test,NBpredictions))</pre></div><div class="section-inner sectionLayout--outsetColumn"><figure name="627b" id="627b" class="graf graf--figure graf--layoutOutsetCenter graf-after--pre"><div class="aspectRatioPlaceholder is-locked" style="max-width: 1000px; max-height: 415px;"><div class="aspectRatioPlaceholder-fill" style="padding-bottom: 41.5%;"></div><img class="graf-image" data-image-id="1*WsijGyIosK6-o5rOWncDxQ.png" data-width="1119" data-height="464" src="https://cdn-images-1.medium.com/max/1000/1*WsijGyIosK6-o5rOWncDxQ.png"></div></figure></div><div class="section-inner sectionLayout--insetColumn"><p name="5f7b" id="5f7b" class="graf graf--p graf-after--figure graf--trailing">The model has an accuracy of <strong class="markup--strong markup--p-strong">97%</strong> which is very good. This model can predict whether the customer liked or disliked the restaurant from the review he posted.</p></div></div></section>
</section>
<footer><p>By <a href="https://medium.com/@kborole7" class="p-author h-card">Kaustubh Borole</a> on <a href="https://medium.com/p/ea500e1ef84d"><time class="dt-published" datetime="2018-10-09T01:27:10.963Z">October 9, 2018</time></a>.</p><p><a href="https://medium.com/@kborole7/web-scraping-yelp-text-mining-and-sentiment-analysis-for-restaurant-reviews-ea500e1ef84d" class="p-canonical">Canonical link</a></p><p>Exported from <a href="https://medium.com">Medium</a> on October 9, 2018.</p></footer></article></body></html>
