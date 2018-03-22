---
id: solr
title: Solr Configuration
sidebar_label: Solr Configuration
---


Dowanload Solr and Extract-
```shell
$ wget http://archive.apache.org/dist/lucene/solr/6.5.0/solr-6.5.0.tgz
$ tar -xvf solr_6.5.0.tar.gz

```

Copy the solr folder form project directory to solr configurations --

```shell
$ cp - r CollaborationSystem/temp/collab home/edx/solr_6.5.0/server/solr/
$ solr_6.5.0/bin/solr start

```

After configurations are done , open

```shell
$ sudo nano CollaborationSystem/search/views.py

```

And add the solr path to path variable inside the file.

See the example --

```python
from django.shortcuts import render, redirect
import pysolr
path= "http://10.129.132.103:8983/solr/collab"
def search_articles(request):
	if request.method == 'POST':
		searchcriteria = request.POST['searchcriteria']
		conn=pysolr.Solr(path)
		articles=conn.search('*'+searchcriteria+'*')
		return render(request, 'search.html',{'articles':articles})



def IndexDocuments(id,title,body,date):
    conn=pysolr.Solr(path)
    docs = [{'id': id,  'title': title, 'body': body ,'created_at' : str(date) }]
    conn.add(docs)
    return
```
