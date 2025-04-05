See [doc/build-\*.md](/doc)m[p]


WikipediaThe Free Encyclopedia
Search Wikipedia
Search
Donate
Create account
Log in

Contents hide
(Top)
Technical overview
Simple request example
Preflight example
Headers

Request headers
Response headers
Browser support
History
CORS vs JSONP
See also
References
External links
Cross-origin resource sharing

Article
Talk
Read
Edit
View history

Tools
Appearance hide
Text

Small

Standard

Large
Width

Standard

Wide
Color (beta)

Automatic

Light

Dark
From Wikipedia, the free encyclopedia
"CORS" redirects here; not to be confused with Continuously Operating Reference Station.
Cross-origin resource sharing (CORS) is a mechanism to safely bypass the same-origin policy, that is, it allows a web page to access restricted resources from a server on a domain different than the domain that served the web page.

A web page may freely embed cross-origin images, stylesheets, scripts, iframes, and videos. Certain "cross-domain" requests, notably Ajax requests, are forbidden by default by the same-origin security policy. CORS defines a way in which a browser and server can interact to determine whether it is safe to allow the cross-origin request.[1] It allows for more freedom and functionality than purely same-origin requests, but is more secure than simply allowing all cross-origin requests.

The specification for CORS is included as part of the WHATWG's Fetch Living Standard.[2] This specification describes how CORS is currently implemented in browsers.[3] An earlier specification was published as a W3C Recommendation.[4]

Technical overview

Path of an XMLHttpRequest (XHR) through CORS.
For HTTP requests made from JavaScript that can't be made by using a <form> tag pointing to another domain or containing non-safelisted headers, the specification mandates that browsers "preflight" the request, soliciting supported methods from the server with an HTTP OPTIONS request method, and then, upon "approval" from the server, sending the actual request with the actual HTTP request method. Servers can also notify clients whether "credentials" (including Cookies and HTTP Authentication data) should be sent with requests.[5]

Simple request example
Suppose a user visits http://www.example.com and the page attempts a cross-origin request to fetch data from http://service.example.com. A CORS-compatible browser will attempt to make a cross-origin request to service.example.com as follows.

The browser sends the GET request with an extra Origin HTTP header to service.example.com containing the domain that served the parent page:
Origin: http://www.example.com
The server at service.example.com sends one of these three responses:
The requested data along with an Access-Control-Allow-Origin (ACAO) header in its response indicating the requests from the origin are allowed. For example in this case it should be:
Access-Control-Allow-Origin: http://www.example.com
The requested data along with an Access-Control-Allow-Origin (ACAO) header with a wildcard indicating that the requests from all domains are allowed:
Access-Control-Allow-Origin: *
An error page if the server does not allow a cross-origin request[6]
A wildcard same-origin policy is appropriate when a page or API response is intended to be accessible to any code on any site. A freely available web font on a public hosting service like Google Fonts is an example.

The value of "*" is special in that it does not allow requests to supply credentials, meaning that it does not allow HTTP authentication, client-side SSL certificates, or cookies to be sent in the cross-domain request.[7]

Note that in the CORS architecture, the Access-Control-Allow-Origin header is being set by the external web service (service.example.com), not the original web application server (www.example.com). Here, service.example.com uses CORS to permit the browser to authorize www.example.com to make requests to service.example.com.

If a site specifies the header "Access-Control-Allow-Credentials:true", third-party sites may be able to carry out privileged actions and retrieve sensitive information.

Preflight example
When performing certain types of cross-domain Ajax requests, modern browsers that support CORS will initiate an extra "preflight" request to determine whether they have permission to perform the action. Cross-origin requests are preflighted this way because they may have implications to user data.

OPTIONS /
Host: service.example.com
Origin: http://www.example.com
Access-Control-Request-Method: PUT
If service.example.com is willing to accept the action, it may respond with the following headers:

Access-Control-Allow-Origin: http://www.example.com
Access-Control-Allow-Methods: PUT
The browser will then make the actual request. If service.example.com does not accept cross-site requests from this origin then it will respond with error to the OPTIONS request and the browser will not make the actual request.

Headers
The HTTP headers that relate to CORS are:

Request headers
Origin
Access-Control-Request-Method
Access-Control-Request-Headers
Response headers
Access-Control-Allow-Origin
Access-Control-Allow-Credentials
Access-Control-Expose-Headers
Access-Control-Max-Age
Access-Control-Allow-Methods
Access-Control-Allow-Headers
Browser support
CORS is supported by all browsers based on the following layout engines:

Blink- and Chromium-based browsers (Chrome 28+,[8][9] Opera 15+,[8] Amazon Silk, Android's 4.4+ WebView and Qt's WebEngine)
Gecko 1.9.1 (Firefox 3.5,[10] SeaMonkey 2.0[11]) and above.
MSHTML/Trident 6.0 (Internet Explorer 10) has native support.[12] MSHTML/Trident 4.0 & 5.0 (Internet Explorer 8 & 9) provide partial support via the XDomainRequest object.[13]
Presto-based browsers (Opera) implement CORS as of Opera 12.00[14] and Opera Mobile 12, but not Opera Mini.[15]
WebKit (Initial revision uncertain, Safari 4 and above,[16] Google Chrome 3 and above, possibly earlier).[17]
Microsoft Edge All versions.[18]
History
Cross-origin support was originally proposed by Matt Oshry, Brad Porter, and Michael Bodell of Tellme Networks in March 2004 for inclusion in VoiceXML 2.1[19] to allow safe cross-origin data requests by VoiceXML browsers. The mechanism was deemed general in nature and not specific to VoiceXML and was subsequently separated into an implementation NOTE.[20] The WebApps Working Group of the W3C with participation from the major browser vendors began to formalize the NOTE into a W3C Working Draft on track toward formal W3C Recommendation status.

In May 2006 the first W3C Working Draft was submitted.[21] In March 2009 the draft was renamed to "Cross-Origin Resource Sharing"[22] and in January 2014 it was accepted as a W3C Recommendation.[23]

CORS vs JSONP
CORS can be used as a modern alternative to the JSONP pattern. The benefits of CORS are:

While JSONP supports only the GET request method, CORS also supports other types of HTTP requests.
CORS enables a web programmer to use regular XMLHttpRequest, which supports better error handling than JSONP.
While JSONP can cause cross-site scripting (XSS) issues when the external site is compromised, CORS allows websites to manually parse responses to increase security.[1]
The main advantage of JSONP was its ability to work on legacy browsers which predate CORS support (Opera Mini and Internet Explorer 9 and earlier). CORS is now supported by most modern web browsers.[24]

See also
Content Security Policy
Cross-document messaging
Cross site leaks
References
 "Cross-domain Ajax with Cross-Origin Resource Sharing". NCZOnline. 25 May 2010. Retrieved 2012-07-05.
 "Fetch Living Standard".
 "WebAppSec Working Group Minutes".
 "Cross-Origin Resource Sharing".
 "Cross-Origin Resource Sharing (CORS) - HTTP | MDN". developer.mozilla.org. 10 May 2023. Retrieved 7 June 2023.
 "CORS errors - HTTP | MDN". developer.mozilla.org. 2023-05-10. Retrieved 2023-07-04.
 [1]. W3.org. Retrieved on 2021-31-07.
 "Blink". QuirksBlog. April 2013. Retrieved 4 April 2013.
 "Google going its own way, forking WebKit rendering engine". Ars Technica. April 2013. Retrieved 4 April 2013.
 "HTTP access control (CORS) - MDN". Developer.mozilla.org. Archived from the original on 2010-05-27. Retrieved 2012-07-05.
 "Gecko - MDN". Developer.mozilla.org. 2012-06-08. Archived from the original on 2012-08-03. Retrieved 2012-07-05.
 Tony Ross; Program Manager; Internet Explorer (2012-02-09). "CORS for XHR in IE10". MSDN. Retrieved 2012-12-14.
 "cross-site xmlhttprequest with CORS". MOZILLA. Retrieved 2012-09-05.
 David Honneffer, Documentation Specialist (2012-06-14). "12.00 for UNIX Changelog". Opera. Archived from the original on 2012-06-18. Retrieved 2012-07-05.
 David Honneffer, Documentation Specialist (2012-04-23). "Opera Software: Web specifications support in Opera Presto 2.10". Opera.com. Retrieved 2012-07-05.
 on July 6, 2009 by Arun Ranganathan (2009-07-06). "cross-site xmlhttprequest with CORS ✩ Mozilla Hacks – the Web developer blog". Hacks.mozilla.org. Retrieved 2012-07-05.
 "59940: Apple Safari WebKit Cross-Origin Resource Sharing Bypass". Osvdb.org. Archived from the original on 2012-07-19. Retrieved 2012-07-05.
 "Microsoft Edge deverloper's guide". 21 December 2023.
 "Voice Extensible Markup Language (VoiceXML) 2.1". W3.org. 2004-03-23. Retrieved 2012-07-05.
 "Authorizing Read Access to XML Content Using the <?access-control?> Processing Instruction 1.0". W3.org. Retrieved 2012-07-05.
 "Authorizing Read Access to XML Content Using the <?access-control?> Processing Instruction 1.0 W3C - Working Draft 17 May 2006". W3.org. Retrieved 17 August 2015.
 "Cross-Origin Resource Sharing - W3C Working Draft 17 March 2009". W3.org. Retrieved 17 August 2015.
 "Cross-Origin Resource Sharing - W3C Recommendation 16 January 2014". W3.org. Retrieved 17 August 2015.
 "When can I use... Cross Origin Resource Sharing". caniuse.com. Retrieved 2012-07-12.
External links
Fetch Living Standard (the current specification for CORS)
Setting CORS on Apache with correct response headers allowing everything through[permanent dead link]
Detailed how-to information for enabling CORS support in various (web) servers
HTML5 Rocks explains how CORS works in detail
Online CORS misconfiguration scanner Archived 2020-08-10 at the Wayback Machine
vte
Web interfaces
Server-side
Protocols	
HTTP v2v3EncryptionWebDAVCGISCGIFCGIAJPWSRPWebSocket
Server APIs	
C NSAPIC ASAPIC ISAPICOM ASPJakarta Servlet containerCLI OWINASP.NET HandlerPython WSGIPython ASGIRuby RackJavaScript JSGIPerl PSGIPortlet container
Apache modules	
mod_includemod_jkmod_lispmod_monomod_parrotmod_perlmod_phpmod_proxymod_pythonmod_wsgimod_rubyPhusion Passenger
Topics	
Web service vs. Web resourceWOA vs. ROAOpen APIWebhookApplication server comparisonScripting
Client-side
Browser APIs	
C NPAPI LiveConnectXPConnectC NPRuntimeC PPAPI NaClActiveXBHOXBAP
Web APIs	
WHATWG	
AudioCanvasDOMSSEVideoWebSocketsWeb messagingWeb storageWeb workerXMLHttpRequest
W3C	
DOM eventsEMEFileGeolocationIndexedDBMSESVGWebAssemblyWebAuthnWebGPUWebRTCWebXR
Khronos	
WebCLWebGL
Others	
GearsWeb SQL Database (formerly W3C)WebUSB
Topics	
Ajax and Remote scripting vs. DHTMLBrowser extensionCross-site scripting and CORSHydrationMashupPersistent dataWeb IDLScripting
Related topics
Frontend and backendMicroservices RESTGraphQLPush technologySolution stackWeb page StaticDynamicWeb standardsWeb API securityWeb application RichSingle-pageProgressiveWeb framework
Categories: Ajax (programming)World Wide Web Consortium standards
This page was last edited on 23 February 2025, at 01:38 (UTC).
Text is available under the Creative Commons Attribution-ShareAlike 4.0 License; additional terms may apply. By using this site, you agree to the Terms of Use and Privacy Policy. Wikipedia® is a registered trademark of the Wikimedia Foundation, Inc., a non-profit organization.
Privacy policyAbout WikipediaDisclaimersContact WikipediaCode of ConductDevelopersStatisticsCookie statementMobile view
Wikimedia Foundation
Powered by MediaWiki

Cross-origin resource sharing

14 languages
Add topic


WikipediaThe Free Encyclopedia
Search Wikipedia
Search
Donate
Create account
Log in

Contents hide
(Top)
Technical overview
Simple request example
Preflight example
Headers

Request headers
Response headers
Browser support
History
CORS vs JSONP
See also
References
External links
Cross-origin resource sharing

Article
Talk
Read
Edit
View history

Tools
Appearance hide
Text

Small

Standard

Large
Width

Standard

Wide
Color (beta)

Automatic

Light

Dark
From Wikipedia, the free encyclopedia
"CORS" redirects here; not to be confused with Continuously Operating Reference Station.
Cross-origin resource sharing (CORS) is a mechanism to safely bypass the same-origin policy, that is, it allows a web page to access restricted resources from a server on a domain different than the domain that served the web page.

A web page may freely embed cross-origin images, stylesheets, scripts, iframes, and videos. Certain "cross-domain" requests, notably Ajax requests, are forbidden by default by the same-origin security policy. CORS defines a way in which a browser and server can interact to determine whether it is safe to allow the cross-origin request.[1] It allows for more freedom and functionality than purely same-origin requests, but is more secure than simply allowing all cross-origin requests.

The specification for CORS is included as part of the WHATWG's Fetch Living Standard.[2] This specification describes how CORS is currently implemented in browsers.[3] An earlier specification was published as a W3C Recommendation.[4]

Technical overview

Path of an XMLHttpRequest (XHR) through CORS.
For HTTP requests made from JavaScript that can't be made by using a <form> tag pointing to another domain or containing non-safelisted headers, the specification mandates that browsers "preflight" the request, soliciting supported methods from the server with an HTTP OPTIONS request method, and then, upon "approval" from the server, sending the actual request with the actual HTTP request method. Servers can also notify clients whether "credentials" (including Cookies and HTTP Authentication data) should be sent with requests.[5]

Simple request example
Suppose a user visits http://www.example.com and the page attempts a cross-origin request to fetch data from http://service.example.com. A CORS-compatible browser will attempt to make a cross-origin request to service.example.com as follows.

The browser sends the GET request with an extra Origin HTTP header to service.example.com containing the domain that served the parent page:
Origin: http://www.example.com
The server at service.example.com sends one of these three responses:
The requested data along with an Access-Control-Allow-Origin (ACAO) header in its response indicating the requests from the origin are allowed. For example in this case it should be:
Access-Control-Allow-Origin: http://www.example.com
The requested data along with an Access-Control-Allow-Origin (ACAO) header with a wildcard indicating that the requests from all domains are allowed:
Access-Control-Allow-Origin: *
An error page if the server does not allow a cross-origin request[6]
A wildcard same-origin policy is appropriate when a page or API response is intended to be accessible to any code on any site. A freely available web font on a public hosting service like Google Fonts is an example.

The value of "*" is special in that it does not allow requests to supply credentials, meaning that it does not allow HTTP authentication, client-side SSL certificates, or cookies to be sent in the cross-domain request.[7]

Note that in the CORS architecture, the Access-Control-Allow-Origin header is being set by the external web service (service.example.com), not the original web application server (www.example.com). Here, service.example.com uses CORS to permit the browser to authorize www.example.com to make requests to service.example.com.

If a site specifies the header "Access-Control-Allow-Credentials:true", third-party sites may be able to carry out privileged actions and retrieve sensitive information.

Preflight example
When performing certain types of cross-domain Ajax requests, modern browsers that support CORS will initiate an extra "preflight" request to determine whether they have permission to perform the action. Cross-origin requests are preflighted this way because they may have implications to user data.

OPTIONS /
Host: service.example.com
Origin: http://www.example.com
Access-Control-Request-Method: PUT
If service.example.com is willing to accept the action, it may respond with the following headers:

Access-Control-Allow-Origin: http://www.example.com
Access-Control-Allow-Methods: PUT
The browser will then make the actual request. If service.example.com does not accept cross-site requests from this origin then it will respond with error to the OPTIONS request and the browser will not make the actual request.

Headers
The HTTP headers that relate to CORS are:

Request headers
Origin
Access-Control-Request-Method
Access-Control-Request-Headers
Response headers
Access-Control-Allow-Origin
Access-Control-Allow-Credentials
Access-Control-Expose-Headers
Access-Control-Max-Age
Access-Control-Allow-Methods
Access-Control-Allow-Headers
Browser support
CORS is supported by all browsers based on the following layout engines:

Blink- and Chromium-based browsers (Chrome 28+,[8][9] Opera 15+,[8] Amazon Silk, Android's 4.4+ WebView and Qt's WebEngine)
Gecko 1.9.1 (Firefox 3.5,[10] SeaMonkey 2.0[11]) and above.
MSHTML/Trident 6.0 (Internet Explorer 10) has native support.[12] MSHTML/Trident 4.0 & 5.0 (Internet Explorer 8 & 9) provide partial support via the XDomainRequest object.[13]
Presto-based browsers (Opera) implement CORS as of Opera 12.00[14] and Opera Mobile 12, but not Opera Mini.[15]
WebKit (Initial revision uncertain, Safari 4 and above,[16] Google Chrome 3 and above, possibly earlier).[17]
Microsoft Edge All versions.[18]
History
Cross-origin support was originally proposed by Matt Oshry, Brad Porter, and Michael Bodell of Tellme Networks in March 2004 for inclusion in VoiceXML 2.1[19] to allow safe cross-origin data requests by VoiceXML browsers. The mechanism was deemed general in nature and not specific to VoiceXML and was subsequently separated into an implementation NOTE.[20] The WebApps Working Group of the W3C with participation from the major browser vendors began to formalize the NOTE into a W3C Working Draft on track toward formal W3C Recommendation status.

In May 2006 the first W3C Working Draft was submitted.[21] In March 2009 the draft was renamed to "Cross-Origin Resource Sharing"[22] and in January 2014 it was accepted as a W3C Recommendation.[23]

CORS vs JSONP
CORS can be used as a modern alternative to the JSONP pattern. The benefits of CORS are:

While JSONP supports only the GET request method, CORS also supports other types of HTTP requests.
CORS enables a web programmer to use regular XMLHttpRequest, which supports better error handling than JSONP.
While JSONP can cause cross-site scripting (XSS) issues when the external site is compromised, CORS allows websites to manually parse responses to increase security.[1]
The main advantage of JSONP was its ability to work on legacy browsers which predate CORS support (Opera Mini and Internet Explorer 9 and earlier). CORS is now supported by most modern web browsers.[24]

See also
Content Security Policy
Cross-document messaging
Cross site leaks
References
 "Cross-domain Ajax with Cross-Origin Resource Sharing". NCZOnline. 25 May 2010. Retrieved 2012-07-05.
 "Fetch Living Standard".
 "WebAppSec Working Group Minutes".
 "Cross-Origin Resource Sharing".
 "Cross-Origin Resource Sharing (CORS) - HTTP | MDN". developer.mozilla.org. 10 May 2023. Retrieved 7 June 2023.
 "CORS errors - HTTP | MDN". developer.mozilla.org. 2023-05-10. Retrieved 2023-07-04.
 [1]. W3.org. Retrieved on 2021-31-07.
 "Blink". QuirksBlog. April 2013. Retrieved 4 April 2013.
 "Google going its own way, forking WebKit rendering engine". Ars Technica. April 2013. Retrieved 4 April 2013.
 "HTTP access control (CORS) - MDN". Developer.mozilla.org. Archived from the original on 2010-05-27. Retrieved 2012-07-05.
 "Gecko - MDN". Developer.mozilla.org. 2012-06-08. Archived from the original on 2012-08-03. Retrieved 2012-07-05.
 Tony Ross; Program Manager; Internet Explorer (2012-02-09). "CORS for XHR in IE10". MSDN. Retrieved 2012-12-14.
 "cross-site xmlhttprequest with CORS". MOZILLA. Retrieved 2012-09-05.
 David Honneffer, Documentation Specialist (2012-06-14). "12.00 for UNIX Changelog". Opera. Archived from the original on 2012-06-18. Retrieved 2012-07-05.
 David Honneffer, Documentation Specialist (2012-04-23). "Opera Software: Web specifications support in Opera Presto 2.10". Opera.com. Retrieved 2012-07-05.
 on July 6, 2009 by Arun Ranganathan (2009-07-06). "cross-site xmlhttprequest with CORS ✩ Mozilla Hacks – the Web developer blog". Hacks.mozilla.org. Retrieved 2012-07-05.
 "59940: Apple Safari WebKit Cross-Origin Resource Sharing Bypass". Osvdb.org. Archived from the original on 2012-07-19. Retrieved 2012-07-05.
 "Microsoft Edge deverloper's guide". 21 December 2023.
 "Voice Extensible Markup Language (VoiceXML) 2.1". W3.org. 2004-03-23. Retrieved 2012-07-05.
 "Authorizing Read Access to XML Content Using the <?access-control?> Processing Instruction 1.0". W3.org. Retrieved 2012-07-05.
 "Authorizing Read Access to XML Content Using the <?access-control?> Processing Instruction 1.0 W3C - Working Draft 17 May 2006". W3.org. Retrieved 17 August 2015.
 "Cross-Origin Resource Sharing - W3C Working Draft 17 March 2009". W3.org. Retrieved 17 August 2015.
 "Cross-Origin Resource Sharing - W3C Recommendation 16 January 2014". W3.org. Retrieved 17 August 2015.
 "When can I use... Cross Origin Resource Sharing". caniuse.com. Retrieved 2012-07-12.
External links
Fetch Living Standard (the current specification for CORS)
Setting CORS on Apache with correct response headers allowing everything through[permanent dead link]
Detailed how-to information for enabling CORS support in various (web) servers
HTML5 Rocks explains how CORS works in detail
Online CORS misconfiguration scanner Archived 2020-08-10 at the Wayback Machine
vte
Web interfaces
Server-side
Protocols	
HTTP v2v3EncryptionWebDAVCGISCGIFCGIAJPWSRPWebSocket
Server APIs	
C NSAPIC ASAPIC ISAPICOM ASPJakarta Servlet containerCLI OWINASP.NET HandlerPython WSGIPython ASGIRuby RackJavaScript JSGIPerl PSGIPortlet container
Apache modules	
mod_includemod_jkmod_lispmod_monomod_parrotmod_perlmod_phpmod_proxymod_pythonmod_wsgimod_rubyPhusion Passenger
Topics	
Web service vs. Web resourceWOA vs. ROAOpen APIWebhookApplication server comparisonScripting
Client-side
Browser APIs	
C NPAPI LiveConnectXPConnectC NPRuntimeC PPAPI NaClActiveXBHOXBAP
Web APIs	
WHATWG	
AudioCanvasDOMSSEVideoWebSocketsWeb messagingWeb storageWeb workerXMLHttpRequest
W3C	
DOM eventsEMEFileGeolocationIndexedDBMSESVGWebAssemblyWebAuthnWebGPUWebRTCWebXR
Khronos	
WebCLWebGL
Others	
GearsWeb SQL Database (formerly W3C)WebUSB
Topics	
Ajax and Remote scripting vs. DHTMLBrowser extensionCross-site scripting and CORSHydrationMashupPersistent dataWeb IDLScripting
Related topics
Frontend and backendMicroservices RESTGraphQLPush technologySolution stackWeb page StaticDynamicWeb standardsWeb API securityWeb application RichSingle-pageProgressiveWeb framework
Categories: Ajax (programming)World Wide Web Consortium standards
This page was last edited on 23 February 2025, at 01:38 (UTC).
Text is available under the Creative Commons Attribution-ShareAlike 4.0 License; additional terms may apply. By using this site, you agree to the Terms of Use and Privacy Policy. Wikipedia® is a registered trademark of the Wikimedia Foundation, Inc., a non-profit organization.
Privacy policyAbout WikipediaDisclaimersContact WikipediaCode of ConductDevelopersStatisticsCookie statementMobile view
Wikimedia Foundation
Powered by MediaWiki

Cross-origin resource sharing

14 languages
Add topic
