# Configure an LDAPS Endpoint for Simple AD
CloudFormation Template that creates 2 EC2 HAProxy instances and an ELB. Please review [the complete blog post](https://aws.amazon.com/blogs/security/how-to-configure-an-ldaps-endpoint-for-simple-ad/) for additional details about this solution.

### Solution Diagram
![](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2017/08/28/Screen-Shot-2017-07-25-at-10.30.54-AM.png)

Here is how the solution works, as shown in the preceding numbered diagram:
1. The LDAP client sends an LDAPS request to ELB on TCP port 636.
2. ELB terminates the SSL/TLS session and decrypts the traffic using a certificate. ELB sends the decrypted LDAP traffic to the EC2 3. instances running HAProxy on TCP port 389.
3. The HAProxy servers forward the LDAP request to the Simple AD servers listening on TCP port 389 in a fixed Auto Scaling group configuration.
4. The Simple AD servers send an LDAP response through the HAProxy layer to ELB. ELB encrypts the response and sends it to the client.
