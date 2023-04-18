# ElasticSearch Operations 01


## Perform multiple operations with _bulk

### First we create new type.

	PUT book
	{
	  "mappings":{
	    "properties":{
	      "book_name":{"type":"text"},
	      "book_author":{"type":"float"}
	    }
	  }
	}

### Now we can add new documents.
		
	PUT _bulk
	{"index":{"_index":"book"}}
	{"book_name":"The 48 Laws Of Power","book_author":"Robert Greene"}
	{"create":{"_index":"book","_id":1}}

<hr>

## Analyzer

Analyzers are the special algorithms that determine how a string field in a document is transformed into terms in an inverted index

<br>

### Now create index with custom filters

	PUT /my-index
	{
	  "settings": {
	    "analysis": {
	      "analyzer": {
	        "my_analyzer":{
	          "type":"custom",
	          "char_filter": [
	            "html_strip"
	          ],
	          "tokenizer":"standard",
	          "filter" : ["lowercase","snowball","stop"]
	        }
	      }
	    }
	  }
	}

### Let's try

	POST my-index/_analyze
	{
	  "text":["The two <em>lazy</em> dogs, were slower than the less lazy <em>dog</em>"],
	  "analyzer": "my_analyzer"
	}

### The output
	
	{
	  "tokens": [
	    {
	      "token": "two",
	      "start_offset": 4,
	      "end_offset": 7,
	      "type": "<ALPHANUM>",
	      "position": 1
	    },
	    {
	      "token": "lazi",
	      "start_offset": 12,
	      "end_offset": 21,
	      "type": "<ALPHANUM>",
	      "position": 2
	    },
	    {
	      "token": "dog",
	      "start_offset": 22,
	      "end_offset": 26,
	      "type": "<ALPHANUM>",
	      "position": 3
	    },
	    {
	      "token": "were",
	      "start_offset": 28,
	      "end_offset": 32,
	      "type": "<ALPHANUM>",
	      "position": 4
	    },
	    {
	      "token": "slower",
	      "start_offset": 33,
	      "end_offset": 39,
	      "type": "<ALPHANUM>",
	      "position": 5
	    },
	    {
	      "token": "than",
	      "start_offset": 40,
	      "end_offset": 44,
	      "type": "<ALPHANUM>",
	      "position": 6
	    },
	    {
	      "token": "less",
	      "start_offset": 49,
	      "end_offset": 53,
	      "type": "<ALPHANUM>",
	      "position": 8
	    },
	    {
	      "token": "lazi",
	      "start_offset": 54,
	      "end_offset": 58,
	      "type": "<ALPHANUM>",
	      "position": 9
	    },
	    {
	      "token": "dog",
	      "start_offset": 63,
	      "end_offset": 71,
	      "type": "<ALPHANUM>",
	      "position": 10
	    },
	    {
	      "token": "rover",
	      "start_offset": 72,
	      "end_offset": 77,
	      "type": "<ALPHANUM>",
	      "position": 11
	    }
	  ]
	}

### What Is Going On In The Background

<li>Remove all HTML tags from the source text via the html_strip char filter. 
<li>Break up the text along word boundaries and remove punctuation with the standard tokenizer.
<li>Lowercase all the tokens.
<li>Remove tokens that are stopwords, such as 'the', 'and' and other irrelevant common words.
<li>Stem all the tokens using the snowball token filter.

<br>

<img src="https://api.contentstack.io/v2/assets/575e4c8c9985d58976376a3c/download?uid=bltee4e0b427d8fdad4?uid=bltee4e0b427d8fdad4">


