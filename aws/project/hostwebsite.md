# We need to take a dummy static website host it in s3 and make it live (access it through url)
   * We will do 5 step..
     Create bucket
     Upload website files
     Enable static website hosting
     Make bucket public
     Open website URL
# ✅ Step 1 — Create S3 Bucket
     *AWS Console → S3 → Create bucket
# step 2 -
     Block all public access
        Click → Create bucket
# step3 -
     ✅  Upload Website Files
         *Create simple files on your laptop:

              index.html
              <html>
              <head><title>My Site</title></head>
              <body>
              <h1>Hello from S3 Static Website</h1>
              </body>
              </html>
# step4 -
     ✅  Enable Static Website Hosting
             Bucket → Properties tab → scroll down
       Click:
           *Static website hosting → Enable
            ✅  Set:
              Index document: index.html
              Error document: error.html (optional)
           ✅   Save.
               You will see a Website endpoint URL — copy it.

   ✅ Step 4 — Make Files Public (Bucket Policy)
        Go to : Permissions → Bucket Policy → Edit
        
     
