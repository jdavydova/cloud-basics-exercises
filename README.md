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
