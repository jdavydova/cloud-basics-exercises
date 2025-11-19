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
