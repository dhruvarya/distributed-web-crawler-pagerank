# DISTRIBUTED WEB CRAWLER WITH PAGE RANK

DHRUV ARYA, VISHAL VERMA
AKASH VERMA, AAKASH DANTRE

## INTRODUCTION

This distributed web crawler uses multithreading to construct the web graph of linking relationships between websites starting at certain root sites provided by the user. The crawler will store this graph in a distributed manner and will be able to respond to several kinds of queries about this graph. 

Page rank is also calculated which is a value assigned to a web page as a measure of its popularity or importance, used to determine the order in which search engine results are presented.

## HOW TO RUN
Code link: https://github.com/dhruvarya/distributed-web-crawler-pagerank
Download the crawler from the link
 
Go to webcrawlermain.go and update siteToCraw and depth variable
```
	siteToCrawl := "https://www.linkedin.com"
	depth := 5
	
```

 
Use commands
```
=> go build
=> go run .
```

## Working
- It creates multiple threads as workers that send requests to root website
- Find each website is created as a node, with page rank, incoming nodes and outgoing nodes as attributes

```
// Node is a node in the graph
type Node struct {
	Id       NodeID
	Rank     float64
	Outgoing map[EdgeID]*Edge
	Incoming map[EdgeID]*Edge
}
```
- extractLinksFromToken function is called from linksextractor.go file that take out the links from a website and return them.
- Clients can initiate the crawling, specifying an initial web page, and can also query the crawled dataset.
- Page rank is calculated using the graph of websites created.


## architecture


![alt text](https://www.cs.ubc.ca/~bestchai/teaching/cs416_2016w2/assign5/arch.png)

The server must handle exactly one client that connects and invokes several RPCs.
The client can invoke four kinds of RPCs against the server:
workerIPsList ← GetWorkers()
workerIP ← Crawl(URL, depth)
domainsList ← Domains(workerIP)
numPages ← Overlap(URL1, URL2)



## PAGE RANK CALCULATION AND PARAMETERS
In the algorithm, we used the formula

![alt text](http://www.strategic-planet.com/wp-content/uploads/2019/12/Figure-2-640x202.jpg)


calculate the new rank based on the current rank and the out-degree, out-degree is the number of neighbors of pr node

```
pr := PageRank{
		Alpha:     0.85,
		MaxIter:   1000,
		Tolerance: 1e-12,
	}
```

Here,
 Alpha is the damping parameter for PageRank, default=0.85.
MaxIter is the max amount of iterations
 Tolerance, (i.e., if you get a new page-rank value that differs from the prior iteration by less than this amount, then stop).




