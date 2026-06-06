This is Amazons own Content Delivery Network (CDN)

What is a CDN? - globally distributed group of servers - called **Edge Locations** that caches web content near to end users - meaning if Servers are hosted in London then someone from Australia doesn't need to wait a very long time to load up your page. Heres how it works: 
	 A user in Sydney visits your site for the very first time. they hit the CDN Edge Location in Sydney. the Edge location looks in its hard drive for content - cant find it - pings London server, pulls files and saves copy locally. 
	 So any subsequent request is instant. 


CloudFront integrates with AWS security like Shield, AWS Web Application Firewall. 


**CloudFront - Origins**: 
an Origin is simply a source of truth where your original, definitive website files and backend Code lives. - So in the Sydney example above - the Origin is London. More specifically it is either one of these two categories: 
- Amazon S3 Buckets (Storage)
  This is the most common use case for static assets. You store your frontend files - like HTML, CSS, JavaScript, images, and videos - in an S3 bucket, and set that bucket as the CloudFront origin.
- Custom Origins (Compute & APIs)
  A custom origin is any server or resource that communicates over HTTP/HTTPS. This is where your dynamic, backend application logic lives. Examples include:

you can also have an ALB or EC2 as an Origin. This means ALB or EC2 must be Public (The SG must allow it).