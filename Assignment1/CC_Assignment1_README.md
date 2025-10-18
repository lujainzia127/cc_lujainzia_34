# CC Assignment 1

**Name:** Lujain Zia  
**Roll No:** 2023-BSE-034  
**Date:** October 12, 2025  

---

## Task 1: Run Gitea in Codespace and Create an Initial Repo

### 1. Set Up Gitea
- Run a Gitea server inside your Codespace.  
- Use HTTPS for communication (SSH is not supported in Codespace).

### 2. Create a Repository
- Create a new repository on your Gitea server.
- Add a `README.md` file listing each student's name and roll number.

### 3. Add Remote Repo
Use the following command to add your Gitea repository as a remote:

```bash
git remote add gitea <your_gitea_repo_https_url>
```

Then push your initial commit containing the `README.md` to Gitea.

---

## Task 2: Mirror README.md from Gitea to GitHub

1. Continue working with your existing repository.  
2. Create a new GitHub repository named `assignment 1`.  
3. Add your GitHub repository as a remote:
   ```bash
   git remote add github <your_github_repo_https_url>
   ```
4. Push the `README.md` file to GitHub:
   ```bash
   git push github main
   ```
5. Verify remotes:
   ```bash
   git remote -v
   ```

---

## Task 3: Use Git LFS for Large Files

### 1. Install Git LFS
Set up Git LFS in your local repository:

```bash
git lfs install
```

### 2. Add Large Files
- Add three files larger than 100 MB each to your repository.  
- Track them using Git LFS:
  ```bash
  git lfs track "*.ext"
  ```
  Replace `.ext` with the appropriate file extension.

### 3. Reference in Assignment Repo
Commit and push these large files to your GitHub repository:
```bash
git add .
git commit -m "Add large files tracked by Git LFS"
git push github main
```

---

## Task 4: Create a Portfolio/CV with GitHub Pages

### 1. Create a New Repository
- Create a new repository named `<your-username>.github.io`.  
  Example: `lujainzia127.github.io`

### 2. Design Your Portfolio/CV
- Create your portfolio or CV using HTML and CSS.  
- You can use a static site generator if preferred.

### 3. Publish with GitHub Pages
- Push your portfolio/CV files to the `<your-username>.github.io` repository.  
- Enable GitHub Pages under **Settings → Pages**.  
- Your live site will be available at:

🔗 **Webpage:** [https://lujainzia127.github.io](https://lujainzia127.github.io)

---

## Repository Links

- **Gitea Repository:** [https://gitea.com/lujainzia127/studentlist](https://gitea.com/lujainzia127/studentlist)  
- **GitHub Repository:** [https://github.com/lujainzia127/assign1](https://github.com/lujainzia127/assign1)

---

## Notes

- Ensure your system meets the minimum requirements for VMware and Ubuntu.  
- Allocate sufficient resources to the VM for smooth operation.  
- Keep the ISO and VMware tools updated.

---

