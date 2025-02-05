# Setting Up Multiple GitHub Accounts with SSH on macOS  

This guide helps you configure **multiple GitHub accounts** using SSH on macOS.  

---

## **1⃣ Generate SSH Keys for Each GitHub Account**  

Run the following commands to create separate SSH keys for each account.  

### **For Account 1 (`user1`)**
```sh
ssh-keygen -t rsa -b 4096 -C "example@mail.com" -f ~/.ssh/github-user1
```

### **For Account 2 (`user2`)**
```sh
ssh-keygen -t rsa -b 4096 -C "example2@mail.com" -f ~/.ssh/github-user2
```

---

## **2⃣ Add SSH Keys to SSH Agent**  

Start the SSH agent:  
```sh
eval "$(ssh-agent -s)"
```

Then add both keys:  
```sh
ssh-add ~/.ssh/github-user1
ssh-add ~/.ssh/github-user2
```

---

## **3⃣ Configure SSH for Multiple Accounts**  

Edit the SSH config file:  
```sh
nano ~/.ssh/config
```

Add the following configuration:  

```ini
# GitHub Account 1 (user1)
Host github-user1
  HostName github.com
  User git
  IdentityFile ~/.ssh/github-user1

# GitHub Account 2 (user2)
Host github-user2
  HostName github.com
  User git
  IdentityFile ~/.ssh/github-user2
```

Save and exit (`CTRL + X`, then `Y`, then `Enter`).

---

## **4⃣ Add SSH Keys to GitHub**  

Copy and add your SSH keys to the respective GitHub accounts.  

For `user1`:  
```sh
pbcopy < ~/.ssh/github-user1.pub
```
For `user2`:  
```sh
pbcopy < ~/.ssh/github-user2.pub
```
Then go to **GitHub → Settings → SSH and GPG Keys → Add New SSH Key**, and paste the key.

---

## **5⃣ Test the Connection**  

For `user1`:  
```sh
ssh -T git@github-user1
```
For `user2`:  
```sh
ssh -T git@github-user2
```
You should see a success message like:  
`Hi username! You've successfully authenticated, but GitHub does not provide shell access.`

---

## **6⃣ Cloning and Pushing with the Correct Account**  

When cloning a repository for **user1**, use:  
```sh
git clone git@github-user1:YourUsername/YourRepository.git
```
For **user2**, use:  
```sh
git clone git@github-user2:YourUsername/YourRepository.git
```

For existing repositories, update the remote:  
```sh
git remote set-url origin git@github-user2:YourUsername/YourRepository.git
```

---

## **✅ Done! 🎉**  

Now your MacBook is set up to handle multiple GitHub accounts with SSH seamlessly. 🚀  