# NoXss
NoXss is a xss scanner, include reflected xss and dom-based xss(used browser). It can scan a single url or many urls from text file, it also support to scan traffic from burpsuite.
# Features
+ Multithreaded
+ Async request(use gevent)
+ Support Dom-based xss(use browser)
+ Support reflected xss
+ Support single url,file and traffic from Burpsuite
+ Traffic filter based on interface
+ Support headers(referer,cookie,e.g.)
+ Support rescan quickly by id
+ Json result
# Directory
```
├── engine.py
├── logo
├── cookie.py
├── url.txt
├── cookie
│   └── test.com_cookie
├── traffic
│   ├── 49226b2cbc77b71b.traffic    #traffic file(pickled)
│   └── 49226b2cbc77b71b.reflect    #reflected file(pickled)
├── config.py
├── start.py
├── url.txt.filtered    #filtered urls
├── util.py
├── README.md
├── banner.py
├── requirements.txt
├── result
│   └── 49226b2cbc77b71b-2019_10_29_11_24_44.json   #result
├── model.py
└── test.py
```
# Screenshot
Noxss:  
![s1](https://github.com/lwzSoviet/download/blob/master/images/s1.png)  
Use browser:   
![s2](https://github.com/lwzSoviet/download/blob/master/images/s2.png)
# Environment
Linux  
Python2.7  
Browser:Phantomjs or Chrome
# Install
1.Make sure that install the browser(chrome or phantomjs) correctly.  
2.pip install requirements
# Usage
```
python start.py --url url --save
python start.py --url url --cookie cookie --browser chrome --save  
python start.py --file ./url.txt --save  
python start.py --burp ./test.xml --save
```
### Options    
**--url**        scan from url.  
**--id**        rescan from *.traffic file by id.  
**--file**        scan urls from text file(like ./url.txt).  
**--burp**        scan *.xml(base64 encoded,like ./test.xml) from burpsuite proxy.  
**--process**        number of process.  
**--cookie**        use cookie.  
**--browser**        use browser(chrome or phantomjs) to scan,it's good at DOM-based xss.  
**--save**        save results to ./result/taskid.json.
### How to rescan
After scanning firstly,there will be taskid.traffic and taskid.reflect in ./traffic/:  
+ taskid.traffic: Web traffic of request(pickled).
+ taskid.reflect: Reflected result (pickled)that included reflected params,reflected position,type and others.  
NoXss will use these middle files to rescan:  
`python start.py --id taskid --save`
### How to scan data from Burpsuite
In Proxy,"Save items" ==> "test.xml"  
![s3](https://github.com/lwzSoviet/download/blob/master/images/s3.png)  
![s4](https://github.com/lwzSoviet/download/blob/master/images/s4.png)  
Then you can scan test.xml:  
`python start.py --burp=./test.xml --save`