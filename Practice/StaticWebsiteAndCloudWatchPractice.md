## Task
Upload HTML/CSS website to S3
Enable static website hosting
Access via public website URL
Check CloudWatch metrics (S3 request metrics)
Explore CloudWatch logs

#### Step -1 Create a simple HTML website
<body>
    <h1>Hello from S3 Static Website Hosting!</h1>
    <p>This site is hosted on Amazon S3.</p>
</body>
</html>

#### Step 2 Upload the website to S3
- Go to AWS Console → S3
- Click your bucket (the same one from previous task)
- Click Upload
- Add index.html
- Click Upload

Files are now in S3 and private

#### Step 3 Enable static website hosting
Now we make S3 behave like a web server.
- In your bucket → go to Properties
- Scroll down to Static website hosting
- Click Edit
- Select: Enable
- Hosting type: Host a static website
- Index document: index.html
- Save changes

#### Step 4 Make the website public
- S3 must allow public READ access for website hosting.
- We do this using a bucket policy.
- Go to Permissions tab
- Scroll to Bucket Policy → Edit
- Update policy (update bucket name)
- Save changes

#### Step 5 Open website
Now open the website URL from the Static website hosting section:
http://<bucket-name>.s3-website-<region>.amazonaws.com

#### Step 6 Explore CloudWatch 
How to view S3 metrics
- Go to AWS Console → CloudWatch
- Left menu → Metrics
- Click S3
- Choose:
-   Storage Metrics
-   Request Metrics
Look for metrics like:
NumberOfObjects, BucketSizeBytes, Requests, 4xxErrors, 05xxErrors

#### Step 7 Explore CloudWatch Logs
S3 does not automatically send logs to CloudWatch.
If you want request logs:
You must enable Server Access Logging (stored in S3)
OR
Use CloudTrail logs (API-level events)

