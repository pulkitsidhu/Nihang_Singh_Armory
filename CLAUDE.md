## Project Overview
I am Nihang Singh, it's my portfolio website to display my swords collection and allow visitors to get in touch. It will be hosted on nihangsingh.com 
See @Project_specs.md for full specifications.

## Important Rules
Always explain like you're talking to a 15 year old with no coding background.
Be as concise as possible. Do not ramble. Less is more
For every response, include:
**What I just did** — plain English, no jargon
**What you need to do** — step by step, assume they've never seen this before
**Why** — one sentence explaining what it does or why it matters
**Next step** — one clear action
**Errors** — if something went wrong, explain it simply and say exactly how to fix it
When a task involves external tools or technical elements that a non-coder wouldn’t know (Supabase, Vercel, Stripe, localhost:3000, etc.):
Walk through exactly where to find what they need (e.g. "go to your Supabase dashboard → Settings → API")
Describe what each key or setting does in one plain sentence
If there's a bucket, folder, or config to create manually, explain what it is and why it exists


## Before Making any changes
Do not assume anything. Ask clarifying questions, interview me when things are not clear.
Before you make any changes, verify how you would test it. 


## Making Changes
After making any code changes, run the relevant tests or start the dev server to check for errors before responding. Never say "done" if the code is untested.
---

## Media Storage — CloudFront CDN

All images and video for this project are served from AWS CloudFront.
Do NOT store media files locally in the repository or reference them as local paths.

**CloudFront base URL:**
https://d31u72jjifwhxm.cloudfront.net

**S3 bucket:** `nihang-singh-armory`
**AWS region:** `us-east-1`

**Media folder structure:**
- https://d31u72jjifwhxm.cloudfront.net/images/  ← all sword photos
- https://d31u72jjifwhxm.cloudfront.net/video/   ← hero video (hero.mp4)

**Image naming convention:**
{sword-slug}-{zero-padded-id}-{photo-number}.jpg
Example: mughal-talwar-001-1.jpg, mughal-talwar-001-2.jpg

**When adding a new sword:**
1. Upload images to S3 first:
   `aws s3 cp {filename} s3://nihang-singh-armory/images/{filename}`
2. Reference in swords.json as full CloudFront URL:
   `https://d31u72jjifwhxm.cloudfront.net/images/{filename}`

**When updating the hero video:**
1. Upload to S3: `aws s3 cp hero.mp4 s3://nihang-singh-armory/video/hero.mp4`
2. CloudFront URL is already set in index.html — no change needed unless filename changes

**Never:**
- Store .jpg, .png, .mp4 files in the GitHub repository
- Reference images as relative paths like `images/filename.jpg`
- Use the S3 bucket URL directly — always use the CloudFront URL