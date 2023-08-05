<h1>SAST using Bandit and in GitLab</h1>


<h2>Description</h2>
This lab focuses on utilizing Bandit, a popular Static Application Security Testing (SAST) tool, within the GitLab platform. Bandit specializes in identifying potential security vulnerabilities in Python applications by performing code analysis and detecting common security issues.

During this hands-on lab, participants will gain practical experience in integrating Bandit into the GitLab pipeline to enhance the security of their Python-based projects. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>Bandit</b>
- <b>JSON</b>
- <b>GitLab</b>

<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>Linux</b> 

<h2>Program walk-through:</h2>

First, we need to download the source code of the project from our git repository: <br/>
```
git clone https://gitlab.practical-devsecops.training/pdso/django.nv webapp
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/5FzQzVk.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s cd into the application so we can scan the app: <br/>
```
cd webapp
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/lhXNJzr.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<br />
<br />

Let’s install the bandit scanner on the system to perform static analysis: <br/>
```
pip3 install bandit==1.7.4
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/46PjQHx.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

We have successfully installed Bandit scanner. Let’s explore the functionality it provides us: <br/>
```
bandit --help
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/U2yO8OU.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let's run the scan. We are using the tee command here to show the output and store it in a file simultaneously: <br/>
```
bandit -r . -f json | tee bandit-output.json
```
<br/>
<p align="center">
<img src="https://i.imgur.com/f5RJxnW.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s run the scan in GitLab in the YAML configuration file: <br/>
```
- docker pull hysnsec/bandit
```
```
- docker run --user $(id -u):$(id -g) -v $(pwd):/src --rm hysnsec/bandit -r /src -f json -o /src/bandit-output.json
```
<p align="center">
<img src="https://i.imgur.com/dSCV5Nu.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>
Here is the result of this job: <br/>
<p align="center">
<img src="https://i.imgur.com/dRy6DzH.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
