# ansible-config-mgt
### Step 1: Install ansible
```bash
sudo apt update
sudo apt install ansible -y
```

### Step 2: Generate a New SSH Key
If you don’t have an SSH key, generate one using:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- Replace `"your_email@example.com"` with the email you use for your GitHub account.
- Press **Enter** to save the key in the default location (`~/.ssh/id_ed25519`).
- Set a passphrase if desired or press **Enter** for none.

### Step 3: Add the SSH Key to GitHub
1. Display your public key:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
2. Copy the output.

3. Go to GitHub:
   - Navigate to **Settings** > **SSH and GPG keys**.
   - Click **New SSH key**.
   - Provide a descriptive title and paste the public key into the **Key** field.
   - Click **Add SSH key**.

### Step 4: Test SSH Connection
Test if your SSH key works with GitHub:
```bash
ssh -T git@github.com
```
You should see a message like:
```plaintext
Hi <username!> You've successfully authenticated, but GitHub does not provide shell access.
```

### Step 5: Push local code to github
1. Create the READMR.md file and push "# ansible-config-mgt"
```bash
echo "# ansible-config-mgt" >> README.md
```

2. Initiate a git repo locally
```bash
git init
```

3. Stage all local files
```bash
git add .
```

4. Commit changes to git
```bash
git commit -m "Project initialization"
```

5. remain the master branch to main
```bash
git branch -M main
```

6. Add the remote repo url to the local repo
```bash
git remote add origin git@github.com:fmanimashaun/ansible-config-mgt.git
```

7. push local changes to guthub
```bash
git push -u origin main
```

>NB: if you run into permission error, run the code `sudo chown -R ubuntu:ubuntu /home/ubuntu/ansible-config-mgt`

### Step 6: Configure a jenkins CI-CD flow for the ansible-config-mgt (optional):
Follow the steps in the [DevOps Tooling Website Deployment with CI/CD - Jenkins](../Projects_documenration/Tooling_website_deployment_automation_with_continuous_integration-jenkins/README.md) on how to configure jenkins job:
1. Create a new freestyle project called `ansible` in jenkins and point it to the `ansible-config-mgt` repo
2. Configure a webhook in Github and set the webhook to trigger ansible build
3. Configure a post-build job to save all (**) files as describes in the [DevOps Tooling Website Deployment with CI/CD - Jenkins](../Projects_documenration/Tooling_website_deployment_automation_with_continuous_integration-jenkins/README.md) project.
4. Test the setup by making some changes to the README.md file.