DevOps CI/CD Pipeline Project 1

Overview

	•	Welcome to the CI/CD (Continuous Integration/Continuous Deployment) project powered by GitHub, Jenkins, Tomcat, and more. This project aims to streamline the development, testing, and deployment processes of applications using modern DevOps practices. 
 
Key Technologies Used:

	•	GitHub: Hosts the source code repository and manages version control.
	•	Jenkins: Orchestrates the CI/CD pipelines, automating builds, tests, and deployments.
	•	Apache Tomcat: Apache Tomcat 9 is an open-source implementation of the Java Servlet, JavaServer Pages, and Java Expression Language technologies, providing a robust and scalable environment for running Java-based web applications.
	•	Apache Ant:  Apache Ant is a Java-based build tool that automates the process of compiling, assembling, and deploying Java applications through an XML-based configuration.

Features:

	•	Automated Builds: Triggered on code commits to GitHub, Jenkins automates the build process using Apache Ant, ensuring consistent and reliable builds.
	•	Continuous Deployment: Deploying a web application in Tomcat 9 involves placing the application's WAR file in the webapps directory, where Tomcat will automatically detect and deploy it.

Purpose:

	•	The purpose of this project is to implement a CI/CD pipeline that automates the build and deployment of a web application using Jenkins, Apache Ant, and Apache Tomcat. The pipeline triggers on code commits, utilizes Jenkins and its plugins for orchestration, employs Apache Ant for build automation, and deploys the resulting WAR file to Tomcat, ensuring efficient, consistent, and reliable application delivery.

Prerequisites

	•	GitHub 
	•	Jenkins
	•	Tomcat 9
	•	Ant

Procedure
1. Install and configure Git, Java, Apache Tomcat 9, Jenkins, Apache Ant.

2. Install all needed plugins in Jenkins like Github, Warning Next Generation, Ant, Unit Realtime Test Reporter, Deploy to container, build pipeline.

3. Clone the project file from Github to local git repo.

4. Create Jenkins Jobs: 
githubpull: 
	•	Set custom workspace & source code management repo url.

buildandcodereview:
	•	Set custom workspace & source code management repo url.
	•	In Build choose Invoke Ant.
	•	In Post build action, select Record compiler warning and static analysis result using Checkstyle tool.

unittest:
	•	Set custom workspace & source code management repo url.
	•	In Build choose Invoke Ant with target junit.
	•	In Post build action, publish junit test results report.

deploy:
	•	Set custom workspace & source code management repo url.
	•	In Build choose Invoke Ant with target war.
	•	In Post build action, select Deploy war/ear to a container & add context path with container tomcat9 & set tomcat url.

5. Jobs Integration:
githubpull:
	•	In Post build action, select Project to build and add buildandcodereview (trigger only if build is stable).
	•	In Poll SCM, schedule it to “* * * * *”

buildandcodereview:
	•	In Post build action, select Build other projects and add unittesting (trigger only if build is stable).

unittesting:
	•	In Post build action, select Build other projects and add deploy (trigger only if build is stable).

6. Create View and start to Build:
	•	Create a Complete Pipeline View using Build Pipeline View, in Upstream/downstream config, select githubpull
	•	Click at Run and in the view it shows the whole process of all the job execution one by one.
	•	Refresh the Tomcat dashboard and the webapp will appear their click that to open the webapp.

Conclusion
This project successfully integrates Jenkins, Apache Ant, and Apache Tomcat to automate the CI/CD pipeline for web application deployment. By leveraging these tools, the pipeline ensures streamlined, consistent, and reliable build and deployment processes, enhancing overall development efficiency.



