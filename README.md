===================== Source bucket policy =====================
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Effect": "Allow",
   "Principal": {
    "AWS": [
     "arn:aws:iam::DIST_ACCOUNT_ID:role/datasync-role",
     "arn:aws:iam::DIST_ACCOUNT_ID:user/distention_account_logged_in_user"
    ]
   },
   "Action": [
    "s3:GetBucketLocation",
    "s3:ListBucket",
    "s3:ListBucketMultipartUploads"
   ],
   "Resource": "arn:aws:s3:::rource_bucket"
  },
  {
   "Effect": "Allow",
   "Principal": {
    "AWS": [
     "arn:aws:iam::DIST_ACCOUNT_ID:role/datasync-role",
     "arn:aws:iam::DIST_ACCOUNT_ID:user/distention_account_logged_in_user"
    ]
   },
   "Action": [
    "s3:AbortMultipartUpload",
    "s3:DeleteObject",
    "s3:GetObject",
    "s3:ListMultipartUploadParts",
    "s3:PutObjectTagging",
    "s3:GetObjectTagging",
    "s3:PutObject"
   ],
   "Resource": "arn:aws:s3:::source_bucket/*"
  }
 ]
}




=================Distention account role policy==================


{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "s3:GetBucketLocation",
                "s3:ListBucket",
                "s3:ListBucketMultipartUploads"
            ],
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::source_bucket"
        },
        {
            "Action": [
                "s3:AbortMultipartUpload",
                "s3:DeleteObject",
                "s3:GetObject",
                "s3:ListMultipartUploadParts",
                "s3:PutObject",
                "s3:GetObjectTagging",
                "s3:ListBucket",
                "s3:PutObjectTagging"
            ],
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::source_bucket/*"
        }
    ]
}




=============== Distention Bucket policy ==================




{
 "Version": "2008-10-17",
 "Statement": [
  {
   "Sid": "DataSyncCreateS3LocationAndTaskAccess",
   "Effect": "Allow",
   "Principal": {
    "AWS": [
     "arn:aws:iam::DIST_ACCOUNT_ID:role/datasync-role",
     "arn:aws:iam::DIST_ACCOUNT_ID:user/distention_account_logged_in_user"
    ]
   },
   "Action": [
    "s3:GetBucketLocation",
    "s3:ListBucket",
    "s3:ListBucketMultipartUploads",
    "s3:AbortMultipartUpload",
    "s3:DeleteObject",
    "s3:GetObject",
    "s3:ListMultipartUploadParts",
    "s3:PutObject",
    "s3:GetObjectTagging",
    "s3:PutObjectTagging"
   ],
   "Resource": [
    "arn:aws:s3:::dist_bucket",
    "arn:aws:s3:::dist_bucket/*"
   ]
  }
 ]
}






===================== AWS CLI command =====================


aws datasync create-location-s3 --s3-bucket-arn arn:aws:s3:::s3-source-01 --s3-storage-class STANDARD --s3-config BucketAccessRoleArn="arn:aws:iam::1234567890:role/datasync-role" --region us-east-1
