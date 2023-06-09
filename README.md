Download Link: https://assignmentchef.com/product/solved-ence360-assignment-1-http-client
<br>
<h1>Part 1 – http client</h1>

Write an implementation of an http client in http.c which performs an HTTP 1.0 query to a website and returns the response string (including header and page content). Note that a server may not respect the range size you specify, so be wary of the webpages you test against. A good one to use is <u>imgur.com</u>.

Make sure to test your implementation against a selection of binary files, and text files – small files and big. Be very careful using string manipulation functions, e.g. <strong>strcpy</strong> – they will not copy any binary data containing a ‘ ’ – so you will want to use the binary counterparts such as <strong>memcpy</strong>.

For downloading bigger files you will need to think about how to allocate memory as you go – functions such as <strong>realloc </strong>allow you to dynamically resize a buffer without copying the contents each time.

Functions which you will need to implement this include: memset, getaddrinfo, socket, connect, realloc, memcpy, perror and free

Also, possibly useful: <strong>fdopen dup</strong>

Your lecture notes may be useful, and this is a good reference which you may find useful: <a href="https://beej.us/guide/bgnet/html/multi/syscalls.html">https://beej.us/guide/bgnet/html/multi/syscalls.html</a>




<h2>Sample HTTP GET request</h2>

To retreive the file <a href="http://www.canterbury.ac.nz/postgrad/documents/cribphdmay.doc">www.canterbury.ac.nz/postgrad/documents/cribphdmay.doc</a>

“GET /page HTTP/1.0r


Host: hostr


Range: bytes=0-500r


User-Agent: getterr
r
”

Where host = “<a href="http://www.canterbury.ac.nz/">www.canterbury.ac.nz</a><a href="http://www.canterbury.ac.nz/">“</a> and page = “postgrad/documents/cribphdmay.doc”. The <em>Range</em> portion is optional, but when specified allows you to retrieve part of a file. See this <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Range_requests">MDN page</a> for more information.




<h2>Example output</h2>

Test programs <strong>http_test</strong>, and <strong>http_download </strong>is provided for you to test your code, an example output of the <strong>http_test </strong>is shown below. It is implemented in <strong>test/http_test.c </strong>and is built by the Makefile by default.  <strong>./http_test www.thomas-bayer.com sqlrest/CUSTOMER/3/  Header:</strong>

HTTP/1.1 200 OK

Server: ApacheCoyote/1.1

ContentType: application/xml

Date: Tue, 02 Sep 2014 04:47:16 GMT

Connection: close

ContentLength: 235

<strong> </strong>

<strong>Content:</strong>

&lt;?xml version=”1.0″?&gt;&lt;CUSTOMER

xmlns:xlink=”http://www.w3.org/1999/xlink”&gt;

&lt;ID&gt;3&lt;/ID&gt;

&lt;FIRSTNAME&gt;Michael&lt;/FIRSTNAME&gt;

&lt;LASTNAME&gt;Clancy&lt;/LASTNAME&gt;

&lt;STREET&gt;542 Upland Pl.&lt;/STREET&gt;

&lt;CITY&gt;San Francisco&lt;/CITY&gt;

&lt;/CUSTOMER&gt;




<strong>http_download</strong> does a similar thing but instead writes the downloaded file to disk using a filename you give  it. A script is provided to test your implementation against those of well known file downloader <strong>wget </strong>

./test_download.sh  <a href="http://www.cosc.canterbury.ac.nz/research/reports/PhdTheses/2015/phd_1501.pdf">www.cosc.canterbury.ac.nz/research/reports/PhdTheses/2015/phd_1501</a>

downloaded 13025535 bytes from

www.cosc.canterbury.ac.nz/research/reports/PhdTheses/2015/phd_1501 .pdf

Files __template and __output are identical

./test_download.sh

static.canterbury.ac.nz/web/graphics/blacklogo.png

downloaded 9550 bytes from

static.canterbury.ac.nz/web/graphics/blacklogo.png Files

__template and __output are identical

<h1>Part 2 – concurrent queue</h1>

Write a classic implementation of a concurrent FIFO queue in <strong>queue.c</strong> which allows multiple producers and consumers to communicate in a thread-safe way.  Before studying the requirements, it is advised to study the test program <strong>queue_test </strong>for an example of how such a queue is intended to be used.

<strong>Hints:</strong> Use semaphores (sem_init, sem_wait, sem_post etc.)  and mutex(s) for thread synchronization. Use a minimum number of synchronization primitives while still maintaining correctness and maximum performance.

<h2>Testing</h2>

A test program <strong>queue_test </strong>is provided for you to test your code and illustrate how to use the concurrent queue.  Note that it is not a completely comprehensive test – and the test used for marking will be much more stringent on correctness, it may be possible to run the queue_test program yet receive low marks. So you may wish to write your own tests and/or test with the provided <strong>downloader </strong>program.

<strong>./queue_test </strong> total sum: 1783293664, expected sum: 1783293664

(This should complete within two seconds on the lab machines)

<h1>Part 3 – chunk sizes &amp; partial-content downloads</h1>

In <strong>http.c, </strong>write an implementation to determine the maximum byte size to request in a partial download.

You should use this to determine the number of partial-content downloads your program needs to execute. A server <em>may not</em> respect the range size. It is recommended to use a <em>HEAD</em> request here since only the headers are desired. The request can be performed similar to a GET request:

“HEAD /page HTTP/1.0r


Host: hostr


User-Agent: getterr
r
”

Where host = ”i.imgur.com” and page =  “VuKnN5P.jpg”

<h1>Part 4 – File Merging &amp; Removal</h1>

In <strong>downloader.c, </strong>two function prototypes have been defined for you. <strong>merge_files</strong> and <strong>remove_chunk_files</strong>. Implement merge_files first, and check that your output is as expected. When your file merging is working correctly, explore removing the partial-download files.

NOTE: Feel free to discard either of these functions and use a more optimal approach (explain this in your report).




<h1>Part 5 – report</h1>

<h2>Algorithm analysis</h2>

Describe the algorithm found in downloader.c (lines 228-264) step by step.

How is this similar to algorithms found in your notes, which is it most like – and are there any improvements which could be made?




<h2>Performance analysis</h2>

Provide a small analysis of performance of the downloader program showing how performance changes as the number of worker threads increases. What is the optimal number of worker threads? What are some of the issues when the number of threads is increased?

Run the downloader several times over different inputs (I have provided some urls e.g. test.txt and large.txt) with small files, and large files to download.

Usage (downloading files in test.txt with 12 threads and saving to directory ‘download’):

./downloader test.txt 12 download

How does the file size impact on performance? Are there any parts of your http downloader which can be modified to download files faster?

A pre-compiled version of the downloader exists in ‘<strong>bin/downloader</strong>‘ how does your implementation compare? If there’s a large discrepancy when the number of threads increase, it’s likely there’s something wrong with your concurrent queue!

Analyse the approach used for file merging and removal. Are there any improvements that can be made? Why? Is the current method of partially downloading every file optimal? If not, suggest a way to improve performance.




<h3></h3>