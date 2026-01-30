# AWS S3(Simple storage Service) ......
  Cloud-based Storage Service that allow you to store,manage
and retrive large amounts of data like files, images,video,and backups securely and at sacle.
It provide highly reliable ,scalable object storage,making your data access from anywhere,anytime,via
the internet.<br>
              1.Store data as objects<br>
              2.Globally unique name<br>
              3.Region specific<br>
              4.Each object within a bucket is stored as a key value pair<br>

# Maximum object Size:
. 5TB (Terabyte) is the maximu size for a single object in Amazon S3.<br>
. Multipart upload is recommended for object large than 5GB upload them Separtely.<br>

# S3 Bucket polices---
Josn-Based access control policies that you attach directly to an S3 bucket to 
managepermissionsfor
accessing the bucket and its objects.They allows you to define who can access the data and what action they can perform,such as read ,write,or delete enabling fine-grained control over the security of your data store in S3.

.Write or paste your JOSN policy in the Bucket policy editor.<br>
.You can use AWS's policy Generator to create a custom policy,or you can manully write the policy 
in JSON format.
           (a). Getobject -- Used to retrieve or download files from an S3 bucket.
           (b). Putobject -- Used to upload or add files into an S3 bucket.

# S3 Versioning ----
It allows you to keep multiple versions of an object in the same bucket, providing protection or overwrites.

# S3 Replication----
IT allows you to automatically copy object from one S3 bucket to another.Which can be--
. Within the same region(Same-Region Relication -SRR)    or
. In diefferent regions(Cross-Region-Replication -CRR)

It's commonly used for compliances,redundancy,and to improve data access performance by maintaining copies closer to your users.


# S3 Storage classes....

(a).S3 Standard (General Purpose): High-throughput, low-latency for frequently accessed data.<br>
(b).S3 Intelligent-Tiering: Automatic cost savings for data with unknown or changing access patterns.<br>
(c).S3 Standard-IA (Infrequent Access): Lower cost than Standard for long-lived, less frequently accessed data.<br>
(d).S3 One Zone-IA: Lower cost than Standard-IA, storing data in a single Availability Zone.<br>
(e).S3 Glacier Instant Retrieval: Archive data requiring milliseconds retrieval.<br>
(f).S3 Glacier Flexible Retrieval (formerly Glacier): Archive data with retrieval options from minutes to hours.<br>
(g)S3 Glacier Deep Archive: Lowest-cost storage, for long-term retention (hours to days retrieval).<br>
(h).S3 Express One Zone: Purpose-built for high-performance, single-zone, frequently accessed data.<br>

# S3 Bucket Lifecycle....
You can use lifecycle policies to control the movement of objects between different storage classes or delete them entirely ,based on specific conditions like age or inactivity.<br>

# S3 Snow family....
1.AWS Snowcone - A small,protable devices for a few terabytes of data.<br>
2.AWS Snowball - A Large device for moving petabytes of data and can also be used for edge computiny.<br>
3.AWS Snowmobile - A massive truck-sized container,typically ued by big companies moving entire data centers.<br>

# Amazon S3 storage Gateway....
It is a hybrid cloud storage services that connection-permises enviorment to cloud storage in Amozon S3.<br>
          1.File Gateway<br>
          2.FSx file Gateway<br>
          3.Tape Gateway<br>
          4.Volume Gateway<br>


