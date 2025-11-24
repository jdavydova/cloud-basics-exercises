#### This project is for the Devops bootcamp exercise for

#### "Cloud Basics"

Use repository: https://gitlab.com/twn-devops-bootcamp/latest/04-build-tools/build-tools-exercises

🔸 [EXERCISE 0: Clone project and create own Git repository]

To work with the project for the exercises:

✅ How to Clone the Provided Project and Create Your Own Git Repository

You were given this repository:
https://gitlab.com/twn-devops-bootcamp/latest/05-cloud/cloud-basics-exercises

Your task:

### - Clone that project
    git clone https://gitlab.com/twn-devops-bootcamp/latest/05-cloud/cloud-basics-exercises.git 
### - Move into the folder:
    cd cloud-basics-exercises
### - Remove the Original Git History
    rm -rf .git
### - If Git doesn't know  name/email

     git config --global user.name "Julia Davydova"
     git config --global user.email "my-mail@gmail.com"
     
 ### - Create your own project/repository using its content    
       git init
       git add .
       git commit -m "Initial commit based on cloud-basic-exercises"
       
### — Create Your Own Remote Repository

Depending on where you want your new repo:
If using GitLab
Go to GitLab ➜ “New Project”
Create an empty repository
Copy the remote URL, e.g.:

https://gitlab.com/your-username/your-new-repo.git


### - Add it as your remote:

    git remote add origin git@github.com:jdavydova/cloud-basics-exercises.git

### - Push your project:

    git push -u origin main

🔸 [EXERCISE 1: Package NodeJS App:]

To have just 1 file, you create an artifact from the Node App. So you do the following:

Package your Node app into a tar file (npm pack)

    cd app/
    npm pack

🔸 [EXERCISE 2: Create a new server:]
Your company uses DigitalOcean as Infrastructure as a Service platform, instead of having on-premise servers. So you:

Create a new droplet server on DigitalOcean

✅ 1. Log into DigitalOcean
Go to: 👉 https://cloud.digitalocean.com
Log in with your company’s or your personal DigitalOcean account.

✅ 2. Click “Create” → “Droplet”
Top-right corner of the dashboard:
Click Create
Select Droplet from the menu

✅ 3. Choose an Image (Operating System)
Common choices:
Ubuntu 22.04 LTS (recommended)
Debian
CentOS
Fedora
For most DevOps exercises, choose:
✔️ Ubuntu 22.04 LTS (x64)

✅ 4. Choose a Plan
For labs or development:

💡 Choose the “Basic” plan.

(2GB RAM) (better for Node.js / Docker / Java exercises)

✅ 5. Choose a Datacenter Region
Select the region closest to you or your users:
New York
Frankfurt
Amsterdam
San Francisco
etc.
Region choice doesn’t affect price.

✅ 6. Authentication Method
You must choose one:
✔️ Option A: SSH Keys (recommended for production)
If you already have an SSH key on your machine:

    cat ~/.ssh/id_rsa.pub

Copy the output and add it to DigitalOcean.
If not, create a new SSH key:

    ssh-keygen -t rsa -b 4096

Then add the key to DigitalOcean.

✔️ Option B: Password (not recommended)
DigitalOcean will email you a root password.

✅ 7. Final Settings

Configure:

Hostname:
example → devops-droplet-1

Tags (optional):
dev, testing, module5, etc.
Backups (optional, extra cost)
Monitoring (recommended ✓)

✅ 8. Create Droplet
Click the Create Droplet button at the bottom.
DigitalOcean will:
provision the VM
assign a public IP
install the OS
start the server
This takes around 30–60 seconds.

🚀 9. Connect to Your New Droplet
Once created, DigitalOcean will show:

Public IPv4
SSH instructions

Connect via SSH:

    ssh admin@my_droplet_ip

🔸 [EXERCISE 3: Prepare server to run Node App:]

Now you have a new fresh server nothing installed on it. Because you want to run a NodeJS application you need to install Node and npm on it:

Install nodejs & npm on it

    sudo apt get -y nodejs npm    

🔸 [EXERCISE 4: Copy App:]
Having everything prepared for the application, you finally:

Copy your simple Nodejs app to the droplet

    scp bootcamp-node-project-1.0.0.tgz admin@167.172.125.11:/admin
    

🔸 [EXERCISE 5: Run Node App:]
Start the node application in detached mode (npm install and node server.js commands)

    tar -zxvf bootcamp-node-project-1.0.0.tgz
    cd package
    npm install
    nohup node server.js > app.log 2>&1 &

Explanation:

    nohup — keeps the process running even after you disconnect from SSH
    > app.log 2>&1 — writes the output and errors into a log file
    & — runs the command in the background

Check running processes:

    ps aux | grep node


Stop the Node.js process:

    pkill node


🔸 [EXERCISE 6: Access from browser - configure firewall]
You see that the application is not accessible through the browser, because all ports are closed on the server. So you:

Open the correct port on Droplet
and access the UI from browser

<img width="1216" height="394" alt="Screenshot 2025-11-21 at 11 08 00 AM" src="https://github.com/user-attachments/assets/9704703a-b0fd-48b1-9db5-1bf71be488f0" />

<img width="862" height="623" alt="Screenshot 2025-11-21 at 10 50 35 AM" src="https://github.com/user-attachments/assets/96321ae7-ac35-43ff-b9b2-fe7a9cbde5cc" />

## Exercises for Module "Artifact Repository Manager with Nexus"

You and other teams in 2 different projects in your company see that they have many different small projects, including the NodeJS application you built in the previous step, the java-gradle helper application and so on. You discuss and decide it would be a good idea to be able to keep all these app artifacts in 1 place, where each team can keep their app artifacts and can access them when they need.

So they ask you to setup Nexus in the company and create repositories for 2 different projects.

🔸 [EXERCISE 1: Install Nexus on a server]

If you already followed the demo in the Nexus module for installing Nexus, then you can use that one.

If not, you can watch the module demo video to install Nexus.

    sudo apt install openjdk-17-jre-headless
    java -version
    cd /opt
    wget https://download.sonatype.com/nexus/3/nexus-3.86.2-01-linux-x86_64.tar.gzc
    tar -zxvf nexus-3.86.2-01-linux-x86_64.tar.gz
    sudo adduser nexus
    sudo chown -R nexus:nexus nexus-3.86.2-01
    sudo chown -R nexus:nexus sonatype-work
    sudo vim nexus-3.86.2-01/bin/nexus.rc
    
        run_as_user="nexus"
    
    su - nexus
    /opt/nexus-3.86.2-01/bin/nexus start
    ps aux | grep nexus

<img width="1205" height="74" alt="Screenshot 2025-11-22 at 10 27 53 AM" src="https://github.com/user-attachments/assets/44d607f6-121f-453f-b7bf-5da8bb0f0ece" />

<img width="864" height="319" alt="Screenshot 2025-11-22 at 10 28 53 AM" src="https://github.com/user-attachments/assets/a457ba29-b4b9-498b-81ad-09127545d0fb" />

Login by admin user with password:

    cat /opt/sonatype-work/nexus3/admin.password

🔸 [EXERCISE 2: Create npm hosted repository]
For a Node application you:

create a new npm hosted repository with a new blob store

<img width="1350" height="700" alt="Screenshot 2025-11-22 at 10 38 33 AM" src="https://github.com/user-attachments/assets/385c1605-9603-49e6-8495-0ff487c2041b" />

<img width="996" height="728" alt="Screenshot 2025-11-22 at 10 41 37 AM" src="https://github.com/user-attachments/assets/9702c16c-7d08-4fd5-9aee-22a7cacde1c9" />

🔸 [EXERCISE 3: Create user for team 1]
You create Nexus user for the project 1 team to have access to this npm repository




