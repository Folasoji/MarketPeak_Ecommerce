Capstone Project: E-Commerce Platform Deployment with git, Linux and AWS
1.	Implement version control with Git;
-	I opened my terminal on vscode, and created my project directory named, MarketPeak_Ecommerce, using the command “mkdir MarketPeak_Ecommerce.”
-	I changed directory to the created directory using command “cd MarketPeak_Ecommerce.”
-	Thereafter, I initialized the git repository with the command “git init”
-	I changed the branch name from master (default) to main by using the command “git branch -m main”.
1.2	I downloaded the recommended website template for e-commerce platform, I extracted the downloaded template into my project directory MarketPeak_Ecommerce. I tried to change the template name to MarketPeak Ecommerce. I could not make much changes on the template.
1.3 stage and commit the template to git:
-	I configured my username and email so that my username and email can be attributed to my work. I used the following commands for this purpose; “git config --global user.name Folasoji, and git config --global user.email folasoji10@gmail.com”
-	I added my website files that I extracted into my project directory (MarketPeak_Ecommerce) to the git repository by staging it with the command “git add .”
-	Afterwards, I checked the status using “git status” to confirm that files have been added and awiting commit. I committed the files to my local repository using the command; “git commit -m “initial commit to setup basic e-commerce website structure”. I used the command “git log” to check the log;
-	$ git log
-	commit d65f2c0ec3643633e3564a23510a6c020513e9f7 (HEAD -> main)
-	Author: Folasoji <folasoji10@gmail.com>
-	Date:   Fri Apr 5 03:26:26 2024 +0000
-	
-	    initial commit to setup basic e-commerce website structure
1.4 Push website files and codes to my github repository
-	For the purpose of review and collaboration, I created a remote repository on my GitHub account.
-	I logged in to my GitHub account and created a new repository named MarketPeak_Ecommerce. I did not include README.md file but I kept it public to aid review and collaboration.
-	With command “git remote add origin https://github.com/Folasoji/MarketPeak_Ecommerce.git” to connect my local repository to my GitHub.
-	I pushed my website files and codes with the command “git push -u origin main” to upload my local repository contents to my GitHub repository I created earlier.
-	PC@DESKTOP-RVR7JSV MINGW64 ~/Desktop/MarketPeak_Ecommerce (main)
-	$ git push -u origin main
-	Enumerating objects: 38, done.
-	Counting objects: 100% (38/38), done.
-	Delta compression using up to 4 threads
-	Compressing objects: 100% (38/38), done.
-	Writing objects: 100% (38/38), 1.85 MiB | 310.00 KiB/s, done.
-	Total 38 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
-	remote: Resolving deltas: 100% (1/1), done.
-	To https://github.com/Folasoji/MarketPeak_Ecommerce.git
-	 * [new branch]      main -> main
-	branch 'main' set up to track 'origin/main'.
-	From above my push request was successful.
2.0	AWS Server (MarketPeak) Deployment .
2.1	AWS EC2 instance Setup;
-	I logged into AWS management console and created EC2 instance using Amazon Linux AMI, free tier.
-	I connected to the EC2 instance successfully using SSH.
-	From my ubuntu terminal, I cd to my Downloads where my keypair was saved.
-	sojy@OlasojiUbuntu:~$ cd Downloads
-	
-	sojy@OlasojiUbuntu:~/Downloads$ chmod 400 "marketpeak.pem"
-	
-	sojy@OlasojiUbuntu:~/Downloads$ ssh -i "marketpeak.pem" ec2-user@ec2-13-50-191-189.eu-north-1.compute.amazonaws.com
-	
-	   ,     #_
-	
-	   ~\_  ####_        Amazon Linux 2023
-	
-	  ~~  \_#####\
-	
-	  ~~     \###|
-	
-	  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
-	
-	   ~~       V~' '->
-	
-	    ~~~         /
-	
-	      ~~._.   _/
-	
-	         _/ _/
-	
-	       _/m/'
-	
-	Last login: Fri Apr  5 16:34:58 2024 from 105.112.230.241
-	
-	[ec2-user@ip-172-31-34-244 ~]$ 
-	I was able to connect to my EC2 instance successfully with above commands.

2.2 Clone the repository on the Linux Server
-	I used ssh-keygen to create key pair (private and public key) to enable me clone my remote repository to AWS EC2 instance.
-	I used the command “cat /home/ubuntu/.ssh/id_rsa.pub” to view my public key.
-	I copied the public key and saved it in my GitHub account. I was prompted tto confirm my password before I could save my public ssh key.
-	With the command “git clone  git@github.com:Folasoji/MarketPeak_Ecommerce.git”, my clone process was completed. I had challenge here because git was not installed on my EC2 instance, but after installation of git with command “sudo yum install git”, I was able to run the git clone command.
2.3	Web Server installation on EC2;
-	I installed apache http server (httpd), a web server that deploys html files and their content on the web. Below commands used;
-	sudo yum update -y (for updating software)
-	sudo yum install httpd -y (for installation of apache)
-	sudo systemctl start httpd (to start apache web server on the EC2 instance)
-	sudo systemctl enable httpd. (for configuration, and start automatically)
This was done successfully.
2.4	configure httpd for website;
•	sudo rm -rf /var/www/html/*
•	sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
•	the first command was to remove default content in the directory /var/www/html, this is because at installation of apache, this directory is created.
•	The 2nd command is to copy website files in my MarketPeak_Ecommerce into the apache directory.
•	“sudo systemctl reload httpd” this command is to reload httpd before launching my web browser.
2.5	Access Website for browsing;
•	I copied my public IP (13.50.191.189) from my EC2 instance and pasted on a blank web and launched with enter key.
•	The browser opened to the landing page.
3.0 Continuous Integration and Deployment Workflow;
•	I created a git branch named development to enable my me work on modifying, adding new features with it affecting the main work. I used the command “git branch development” to create the branch, and “git checkout development” to switch to the branch.
•	I opened the index.html file and edited, company name, social media handles, phone number.
•	I run “git status” to see the file I worked on is yet to be added to staging area after I saved my changes.
•	“git add . to stage changes made, “git commit -m “change of company name, phone number, social media handle”
•	“git push origin development was used to push changes made to my remote repository.
•	I went to my github platform to create a pull request; I reviewed changes made and made comment of few changes and satisfaction.
•	 On my terminal, I changed back to main branch with command; “git checkout main.
•	I proceed to merge the development branch with the main branch with command “git merge development
•	Then I pushed the merged changes to the remote repository with “git push -u  origin main”
•	I used git log to see all my pushed files to the remote repository.
•	I pull again using “git pull origin main but was prompted that no new pull required.
•	With this I was able to successfully work from different branch I created apart from the main branch, made changes and pushed to the remote repository for collaborative review by another. I was able to merge without issues.
•	I ran this command “sudo systemctl reload httpd” to restart the server to effect changes earlier made.
•	I tested the browser again to see whether the changes were effected. Although, it was only the file name that changed, as I am still learning how to edit website template.
I did not encounter any challenges apart from when I was unable to run the clone command on EC2 instance, on slack, Solomon Onwuasoanya helped me out.


I created a README.md file and provided full description of the project there.