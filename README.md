---Phishing URL Detector

Give it a URL, get a phishing probability. Random Forest on ~80 features.

--Feature pipeline (in order)
1. URL length: total, host, path, query, length class
2. Page content (HTML): anchor URLs (`#`, `javascript:`, external), links in `<meta>/<script>/<link>`, external images, **Server Form Handler** (blank / `about:blank` / other domain), password forms
3. Behaviour HTTP + meta-refresh + JS **redirects**, **pop-ups** (`window.open`, `prompt`), **right-click disabled**, **hidden/zero-size iframes**, status-bar tampering
4. Domain reputation: **domain age** (WHOIS), **DNS records** (A/MX/NS/TXT, TTL), TLS cert age, **web traffic** rank (Tranco list), **page rank** (Open PageRank API)
5. URL string features (always on, ~40 features): IP host, `@`, dashes, dots, subdomain depth, suspicious TLDs, shorteners, entropy, digit ratio, brand keywords, punycode, encoded chars, path depth, etc.
data set used -Kagglehub 
The model gets about 97% accuracy on this dataset. These results are for the random forest .
The dataset has 11,055 rows and 30 features, and 44.3% of the rows are phishing.20% of the rows were held for testing.

Metric	                                         Result
Accuracy	                                    96.97%
Phishing precision / recall                 	96.6% / 96.5%
Legitimate precision / recall	                97.2% / 97.3%
ROC-AUC                                     	0.9962
5-fold cross-validation accuracy	            96.35% (±1.0%)

On the 2,211 test rows, the model made 33 false alarms (legitimate sites flagged as phishing) and missed 34 phishing sites.
The most important features were SSLfinal_State (34%) and URL_of_Anchor (26%). web_traffic, having_Sub_Domain and Prefix_Suffix followed.
