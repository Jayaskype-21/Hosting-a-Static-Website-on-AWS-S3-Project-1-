# Hosting-a-Static-Website-on-AWS-S3-Project-1-
A simple static website (HTML/CSS, no server-side code) deployed to an S3 bucket configured for static website hosting. The bucket’s objects are made public by a bucket policy  for improved security and performance.

# Create S3 bucket & enable static website hosting
STEP-1:	AWS Console → S3 → Create bucket.
o	Give a globally unique bucket name (example: my-static-site-<yourname>).
o	Region: choose one close to your users.
o	Uncheck Block all public access if you plan to make objects public through a bucket policy 

STEP-2: Create the bucket.

STEP-3:	In the bucket, go to Properties → Static website hosting → Edit → Enable → Host a static website.
o	Index document: index.html
o	Error document: error.html (optional)
o	Save changes.

STEP-4:	Note the Bucket website endpoint (URL). You will use this to verify the site.

# Bucket policy (make objects publicly readable)

Important security note: Making the bucket public exposes objects to the world. For production or better security, use CloudFront with an Origin Access setting OR grant only the CloudFront Origin Identity access instead of making bucket objects public.

If you want public objects for a quick demo, paste this into Permissions → Bucket policy (replace the ARN):

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Static_Hosting",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-static-site-<yourname>/*"
    }
  ]
}
Replace my-static-site-<yourname> with your bucket name

# Upload site files
•	Use the S3 Console Upload button and upload index.html, error.html, and the assets folder.

# Test the website
Open the Bucket website endpoint (example http://my-static-site-<yourname>.s3-website-us-east-1.amazonaws.com) in your browser. The index.html should load.
To test the error page, navigate to a URL that doesn’t exist (e.g., /missing.html) — S3 will return the error.html content.

# Troubleshooting tips
•	If you see AccessDenied when visiting the website endpoint, check the bucket policy and object ACLs.
•	Make sure index.html is present and named exactly as configured.

