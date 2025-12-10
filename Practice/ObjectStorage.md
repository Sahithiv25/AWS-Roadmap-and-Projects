## Task
Create an S3 bucket → Upload files → Enable/disable public access → Add bucket policy → Learn S3 URLs

#### Step 0 Quick decisions
- Decide the region
- Bucket name (must be globally unique, all lower case, no spaces)

#### Step 1 Create an S3 bucket
- Go to AWS Console → S3
- Click Create bucket
- Fill:
-   Bucket name: aws-learning-s3
-   Region: e.g. US East
- Block Public Access settings → leave ON for now (default).
- Leave everything else as default.
- Click Create bucket

#### Step 2 upload files to the bucket
- Click your bucket: aws-learning-s3
- Click Upload
- In Files, add:
-   e.g. hello.txt or test-image.png
- Scroll down → click Upload

Now you have objects in bucket.
Objects in S3 are files with keys and metadata; they live inside buckets.

#### Step 3 understand and control Public access
Right now, your bucket is fully private.
A. Confirm public access is blocked
    In the bucket, go to Permissions tab.
    You’ll see:
        "Block public access (bucket settings)” → all checkboxes likely ON. 
This means:
Even if you try to make an object public, S3 will block it.
Good for security in real systems.
B. For learning: allow public access (temporarily)
Only do this for a learning bucket with non-sensitive test files.
    In Permissions → Block public access
    Click Edit
    Uncheck: “Block all public access”
It will show a warning → type confirm
Click Save

Now your bucket can be made public using a bucket policy or ACL, but it’s still not public yet.

#### Step 4 - Add a bucket policy to allow public read
We’ll make all objects in this learning bucket readable publicly. This is very common for static websites and public assets.
- Still in Permissions tab
- Scroll to Bucket policy
- Click Edit or Add bucket policy
- JSON 

{
  "Version": "YYYY-Mm-DD",
  "Statement": [
    {
      "Sid": "AllowPublicReadForLearning",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::bucket-name/*"
    }
  ]
}
Then click Save changes.

#### Step 5 Learn & test S3 Object URLs
Now we’ll see the file publicly from the browser.
- Go to your bucket → Objects tab
- Click your object, e.g. hello.txt
- On the object page, find Object URL
I’ll look like:
https://bucketname.s3.us-east-1.amazonaws.com/hello.txt
Copy that URL → open in your browser
If everything is correct, you’ll see:
the text file content, or your image in the browser

#### How to Re-lock if
After you finish learning:
Remove or tighten the bucket policy (e.g., delete it)
Turn Block public access back ON