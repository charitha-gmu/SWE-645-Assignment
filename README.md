<!-- 
  Sree Charitha Meka  
  G01410061
-->

Homepage URL - http://charithaswe645assignment1.s3-website-us-east-1.amazonaws.com/

Student survey Form Url - http://ec2-52-91-50-174.compute-1.amazonaws.com/SWE-645-Assignment-1-Part-2/
username - "admin"  password- "password"

Instructions to Deploy the Student Survey form on tomcat
1. Create a HTML and css file with the given specifications.
2. Add a pom.xml file and a folder WEB-INF with a web.xml in the folder where the html and css files are present.
3. Now create a war file using the command mvn package.
4. Now zip the html, css files along with the war file created in the target folder.
5. Create an EC2 instance on aws using Apache Tomcat packaged by Bitnami Amazon Machine Image by selecting the free tier.
    a. After clicking on launch instance button give the name.
    b. Search for the tomcat by bitnami AMI in AWS Marketplace.
    c. In the instance type select the t2.micro which is eligible for free tier.
    d. Select a key-pair if already existing or create a new key-pair but giving an appropriate name.
    e. Now click on launch instance button to create an instance.
6. Give 400 permissions for the pem key.
7. Now log in to the server using the command ssh -i [pem-key] bitnami@[Public IPv4 DNS]
8. In server, Do cd /opt/bitnami/tomcat
9. Now we are in the tomcat folder, Now add the the role and password in tomcat-users.xml file which is on conf folder (cd conf)
To add the user role and password add the below code in the file (vi tomcat-users.xml)
<role rolename="manager-gui"/>
<user username="admin" password="password" roles="manager-gui,admin-gui"/></tomcat-users>

10. Now from the home path, go to /opt/bitnami/tomcat/webapps/manager/META-INF
In the context.xml file which is in META-INF
Change the value of allow attribute of the Valve tag to "^.*$" (Use sudo vi context.xml command to edit it)

11. Now copy the zip file which contains all our source files and war file using the scp command. (scp -i  [path-to-pem-key-file] [path-to-zip-file] bitnami@[Public IPv4 DNS]:/home/bitnami/[zip-file-name])

12. Now in server (In path home/bitnami) unzip the file we uploaded (unzip [zip-file-name])
13. Now move the unzipped folder to webapps folder in the tomact folder  (sudo cp -r [zip-file-name] /opt/bitnami/tomcat/webapps/)
14. Now in [Public IPv4 DNS] website , Select manage app -> Enter the username and password we have give in tomcat-users.xml file.
15. Click on the website we uploaded and we should see the student survey form.