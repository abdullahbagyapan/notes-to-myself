# ElasticSearch Operations 02



## Queries

### match_phrase

Return if field match fully

	 "query": {
	    "match_phrase": {
	      "book_author":"Introduction To Algorithms"
		 }
	  }


### match

Can return multiple result depends on score('match score')

	"query": {
	    "match": {
	      "book_name":"Introduction To Algorithms"  
	    }
	 }

### match_phrase_prefix

Return if 'field' start with 'phrase'

	"query": {
	    "match_phrase_prefix": {
	      "book_name": "Introduction"
	    }
	}

### match_all

Return all documents
	
	"query": {
	    "match_all": {}
	 }
	




