| Concept     | Explanation                                                     | Important for Exam           |
| ----------- | --------------------------------------------------------------- | ---------------------------- |
| Signed URLs | Used to **restrict access to private content** in CloudFront    | Very common exam topic       |
| Signer      | Entity that **creates the signed URL**                          | Uses a private key           |
| Public key  | Stored in **CloudFront**                                        | Used to verify the signature |
| Private key | Used by the **application** to sign the URL                     | Must be kept secret          |
| Signature   | Added to the URL to prove it was signed by an authorized signer | Grants temporary access      |
