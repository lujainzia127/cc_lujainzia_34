# Cloud Computing – Assignment 1  

**Name:** Lujain Zia  
**Roll No:** 2023-BSE-034  
**Date:** October 12, 2025  

---

## 🧩 Task 1 — Run Gitea in Codespace and Create an Initial Repo  

### 1. Set up Gitea  
- Run a Gitea server inside your Codespace.  
- Use **HTTPS** for communication (SSH is not supported in Codespace).  

### 2. Create a Repository  
- Create a new repository on your Gitea server.  
- Add a `README.md` file listing each student's name and roll number.  

### 3. Add Remote Repo  
Add your Gitea repository as a remote and push the initial commit:
```bash
git remote add gitea <your_gitea_repo_https_url>
git push -u gitea main
```

---

## 🪄 Task 2 — Mirror README.md from Gitea to GitHub  

### 1. Continue Working with Your Existing Repository  
Use the same repository you created and pushed to Gitea in Task 1.  

### 2. Create a GitHub Repository  
Create a new repository named **Assignment-1** on GitHub.  

### 3. Add GitHub as a Second Remote  
```bash
git remote add github <your_github_repo_https_url>
```

### 4. Push the README.md File to GitHub  
Push contents from your local repo to GitHub.  

### 5. Verify Remotes  
Check that both remotes exist:
```bash
git remote -v
```

✅ You should see both **gitea** and **github** listed.

---

## 💾 Task 3 — Use Git LFS for Large Files  

### 1. Install Git LFS  
```bash
git lfs install
```

### 2. Add Large Files  
Add three files larger than 100 MB and track them:
```bash
git lfs track "*.ext"
```
*(Replace `.ext` with the actual file extension, e.g. `.bin`, `.zip`, `.mp4`.)*

### 3. Reference in Assignment Repo  
Commit and push the tracked files:
```bash
git add .
git commit -m "Add large files tracked with Git LFS"
git push origin main
```

---

## 🌐 Task 4 — Create a Portfolio / CV with GitHub Pages  

### 1. Create a New Repository for GitHub Pages  
Create a repository named:
```
<your-username>.github.io
```
For example: `lujainzia127.github.io`

### 2. Design Your Portfolio / CV  
- Create your portfolio or CV using HTML and CSS (or a static site generator).  

### 3. Publish with GitHub Pages  
- Push your website files to the `<your-username>.github.io` repository.  
- Enable GitHub Pages in repository settings (if not automatically enabled).  
- Share your published site link.  

---

## 🔗 Links  

- **Webpage:** [https://lujainzia127.github.io](https://lujainzia127.github.io)  
- **Gitea Repository:** [https://gitea.com/lujainzia127/Assignment-1.git](https://gitea.com/lujainzia127/Assignment-1.git)  
- **GitHub Repository:** [https://github.com/lujainzia127/Assignment-1.git](https://github.com/lujainzia127/Assignment-1.git)
