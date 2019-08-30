# benign-phishing-url-classification-using-whois-and-lexical-features
To identify and extract features from URL that help classify URLs into benign/phishing and train an ML model with these features for classification.

# Assignment Problem Statement

Researching and collecting an appropriate set of benign URLs and phishing URLs.  To train your classifier you will need to extract a set of features from each URL. Researching and selecting an appropriate set of features for extraction forms this task.

Credit will be given for incorporating dynamic features (i.e. ones not generated directly from the URL). You might for example use Python to programmatically perform DNS and/or whois lookups on a domain and transform the resultant answers into features associated with each URL. The choice of features is up to you and part of the research. Your report should include an assessment of which features were found to be most salient.

Your research will reveal that a variety of machine learning algorithms have been applied to the URL classification problem. Credit will be given for comparing the performance of 2-3 such algorithms in your paper.

# Solution

## Features
We divided the features into two categories: Dynamic Features and Lexical Features. 

### A. Dynamic Features 

1. whois features: whois can be performed through python’s whois module. whois python module gives us many information about the URL such as – domain name, registrar, whois_server, creation_date, updated_date, expiration_date, name_servers, emails, etc. Amongst these, the feature on dates i.e., creation_date, updated_date and expiration_date were found to be the most salient. 

Reasons being: 

o creation date validates most of the benign URLs. The older the URL more the chances of it being benign. 
o Most hackers don’t keep their domains running for longer periods. Hence, expiration date will be useful. 
o Similarly, updated date, in combination with creation / expiration date, can show genuinity of a URL. 

Other features like zip code and address, that could have potentially been used for classification, were returned as null for most of the URLs, both benign and malicious, for the dataset we used. Hence, only the date features were finally extracted and used for classification. 

whois module of python, in our opinion, still has scope for development. For example, whois on google.com doesn’t return Registrar URL feature at all since the python module doesn’t hold the key for it. Had this key / feature been available in python whois module, we could have performed a whois on that Registrar URL value to find out if there was a back reference to “google.com” or explored other results. Even a simple absence of the Registrar URL feature could classify some URLs maybe. Likewise, there are many such features that are available in other whois websites but not available in the whois python module. A fully developed python module can be more powerful in dynamically classifying URLs. 

2. nslookup features: nslookup can be performed with the help of python’s DNS resolver module. DNS resolver helps us get results such as the type of IP address ( IPv4 or IPv6 ), MX details (provides information on mail server for the zone ), NS details ( provides information on name servers associated with the zone) and PTR details ( for reverse lookups ) among others. However, in our work we found that many URLs that were reachable to whois were not reachable to DNS resolver and vice versa - leading to shrinkage of workable dataset size. Since most of the URLs were whois responsive, we had to trade using only whois features for using both whois and DNS resolver features. Also, DNS resolver mostly yields features about the zone; which is more general compared to the whois results. Hence, in our study we only used whois features and dropped DNS resolver features

### B. Lexical Features 

Malicious URLs and domains show certain characteristics that cannot be seen in any benign URLs. For an instance the length of the URL. Phishing websites tend to have a lengthy URL consisting of a long query string which will lead users to phishing websites. These phishing websites may ask user to enter credit card details. We also noticed that few phishing URLs contain more than one protocol - which is basically a link to some other malicious website appended as a query string. It was useful that we extracted this feature, Protocols Count, which has never been done in any of the previous research works so far. We captured such features of a URL by studying the lexical content of each URL. Some of the lexical features captured are Dot Count, URL Lenght, Digits Count, Special Characters Count, Hyphen Count, Double Slash Count, Single Slash Count, @ Sign Count, Protocols Count, etc.

## Classifiers

From the results we can note that Random Forest, Decision Tree and KNN are the top three performers amongst all evaluated classifiers. Random Forest achieved the best results by gaining accuracy of 87.85%. It misclassified only 243 URLs out of 2000 URLs on which we predicted.

However, Logistic Regression, Naïve Bayes and SVM are the bad performers amongst all the evaluated classifiers achieving accuracy score less than 80%. Naïve Bayes obtained the least accuracy of 69% which sits at the last position. The bad performing algorithms owes its bad results to the virtue of the algorithms being basic and naive. The top performers owes its good results to the recursive approach of their algorithms.

# Report

Please find the detailed report attached in repo.
