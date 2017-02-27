The present package contains the code for a web Crawler written in Javascript using Nginx as web proxy.
The language has been chosen considering that for this task was more suitable something web-oriented, powerful with string manipulation (possibly regexp) and eventually easy to show graphical results (also for testing purpose). About the last point to reduce complexity was better a client-side language, so Javascript was a good candidate.
As approach to the implementation has been chosen an incremental (agile) one with roughly the following steps:
1. Define the data structure and main functions to support the crawler search and results storage 
2. Define a minimal layout of the page and results presentation that supports the objectives of the application (no fancy)
3. Incrementally enrich the functionalities defined until reaching the objectives set (or an acceptable approximation)

As data structure has been chosen a tree (generic non binary) that is the best model for a site with its pages and resources. 
There are many well-known alghoritms on trees, so instead of writing from scratch is possible take an existing one and adapt in this case (this simplify also considerations on performance/memory especially for the tree).
Once adapted the algorithm for what needed (traverse pre-order instead of DF/BF, extract level for printing) the main problem came with the "same domain policy" that doesn't allow to use javascript on external domain. This limitation has been overcomed using Nginx not only as webserver but also as proxy, anyway the security concerns behind the policy should be considered carefully (see below).
To simplify the implementation some trade-off has been addressed:
- Analysing the page has not been considered some specific internal link that doesn't contain the domain (e.g. "/about") as internal link, they has been store anyway as external links
- Only images has been considered as static content 
- links are matched using http scheme in the content of the page (also if the page itself coudl be https)
- Jquery has been used for retrieving the target pages in non-asynchronous mode (to avoid complex sync on parallel calls)

IMPROVEMENTS
Beside the trade-off made that can be overcome with more time, main improvements are:
1. Avoid the use of the proxy also because the site running this application could be put in black list as considered suspicious or fraud site by Google 
2. substitute the resolver directive in nginx. Also in this case for security reasons should be used a local resolution or a DNS properly configured
3. Adapt the application to crawl wiprodigital.com :). Actually the wipro gives error when tested (instead it worked with apache.org and facebook.com). Probably the proxy cause the requests from the application to be blocked by wipro.
4. Enrich the graphical layout eventually removing the textarea. The data structure is suitable to store all the information necessary to present effectively the resutls in collapsing views or trees.
5. Add format and validation checks and improve the quality of the parsing with the regexp.


INSTALLATION INSTRUCTIONS
Note: the following has been tested on an Ubuntu linux machine in AWS.
Ensure you have installed Nginx and optionally Apache (the 'nginx_site' file assume Apache installed with php, anyway this is not a pre-requisite for the application).

Copy the file 'fillTree.htm' in the root of your Nginx/Apache server (here assumed /var/www/) together with the folder 'js'.
Copy the file 'nginx_site' in the sites folder of the Nginx (here assumed /etc/nginx/site-enabled/)

EXECUTION INSTRUCTIONS
Open in a browser (tested in Chrome) the page fillTree.htm (e.g. http://mydomain/fillTree.htm). 
Insert in the Web Address field the domain without http/https scheme (e.g. apache.org).
Click Add to see the site tree populated in the textarea below.

