This repo contains an exercise code for a web Crawler written in Javascript using Nginx as web proxy.
As data structure it has been chosen a tree (non binary) to leverage existing algorithms to populate and traverse the data structure. 
Nginx has been used both as a proxy and as a webserver to host the application.
During the implementation some limitations has been introduced:
- some common internal links that doesn't contain the domain (e.g. "/about") has been stored ayway as external links (prefixing the domain as necessary)
- For simplicity only images has been considered as static content 
- links are matched using http scheme in the content of the page (even if the page itself could be https)
- Jquery calls have been used for retrieving the target pages in non-asynchronous mode (to avoid complex sync on parallel calls)

TODO
1. Fix the limitations refining data structures and application architecture 
2. Enrich the graphical layout eventually removing the textarea. The data structure is suitable to store all the information necessary to present effectively the resutls in collapsing views or trees.
3. Add format and validation checks and improve the quality of the parsing with the regexp.
4. Substitute the resolver directive in nginx: for security reasons should be used a local resolution or a DNS properly configured
5. Review/Modify the use of the proxy 


INSTALLATION INSTRUCTIONS
Note: the following has been tested on an Ubuntu linux machine installed in AWS.
Ensure you have installed Nginx and optionally Apache (the 'nginx_site' file assume Apache installed with php, anyway this is not a pre-requisite for the application).

Copy the file 'fillTree.htm' in the root of your Nginx/Apache server (here assumed /var/www/) together with the folder 'js'.
Copy the file 'nginx_site' in the sites folder of the Nginx (here assumed /etc/nginx/site-enabled/)

EXECUTION INSTRUCTIONS
Open in a browser (tested in Chrome) the page fillTree.htm (e.g. http://mydomain/fillTree.htm). 
Insert in the Web Address field the domain without http/https scheme (e.g. apache.org).
Click Add to see the site tree populated in the textarea below.

