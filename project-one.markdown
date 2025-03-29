---
layout: page
title: "Project - Jekyll"
permalink: /project-jekyll/
image: "assets/images/img_proj_one.jpg"
---

Welcome to my portfolio project hosted on GitHub Pages. This repository showcases my personal and professional projects, providing an in-depth look into my skills, experiences, and accomplishments.

## Creating My Online Portfolio with GitHub Pages, Jekyll, and the Basically Basic Theme

I created my [GitHub account](https://github.com/danebarnes) back in **2014** when I was first introduced to **version control**, especially for managing code and web development projects. I learned to use **Git**, a command-line tool created by Linus Torvalds, which allows developers to track changes, collaborate with others, and revert back to previous versions of their projects. Git is like a time machine for your code—essential for any serious developer.

### Setting Up Jekyll Locally

To begin building my portfolio site, I installed **Jekyll** on my computer using the **recommended installer** from the [official Jekyll website](https://jekyllrb.com/docs/installation/). Once installed, I ran the following command in the terminal to scaffold a new project:

```bash
jekyll new odiane-portfolio
```

This simple command created a complete folder structure with all the necessary files for a basic static website. With minimal effort, I had a working site that I could preview locally.

Jekyll sites are built using **Markdown** and **YAML**:

- **Markdown** is a lightweight markup language that lets you format text using plain syntax, making it easy to write clean, readable documents for pages and blog posts.
- **YAML** (YAML Ain’t Markup Language) is a configuration language used in the front matter of each page or post to define metadata such as layout, title, permalink, and more.

Jekyll is both beginner-friendly and powerful. It enables users to launch a simple website quickly, yet provides plenty of flexibility and customization options. Thanks to its strong community, there are many themes available. I chose the [Basically Basic theme](https://github.com/mmistakes/jekyll-theme-basically-basic?tab=readme-ov-file#skin) by [@mmistakes](https://github.com/mmistakes), which perfectly matched my vision—a minimalist theme that places the focus on content.

### Hosting with GitHub Pages

I decided to host my portfolio on **GitHub Pages**, which allows you to serve static websites directly from a GitHub repository. Since I had prior experience with Git, setting this up was straightforward.

#### Step 1: Create the project folder and initialize Git

I navigated to my project folder and initialized Git from the command line:

```bash
cd odiane-portfolio
git init
```

#### Step 2: Create the GitHub repository

I then created a new GitHub repository named:

```
danebarnes.github.io
```

This naming is intentional—GitHub recognizes it as a **user site** and serves it at [https://danebarnes.github.io](https://danebarnes.github.io).

#### Step 3: Connect the local folder to GitHub

Next, I connected my local Git folder to the remote GitHub repository:

```bash
git remote add origin git@github.com:danebarnes/danebarnes.github.io.git
```

Since I use **SSH** for secure communication, I ensured my SSH keys were generated and added to GitHub:

```bash
ssh-keygen -t rsa -b 4096 -C "odaine.barnes@gmail.com"
```

I copied the public key to GitHub under **Settings > SSH and GPG Keys**.

#### Step 4: Commit and push the project

After making sure everything was set up, I pushed the files to GitHub:

```bash
git add .
git commit -m "Initial commit"
git push -u origin master
```

#### Step 5: Enable GitHub Pages

Finally, I went into the GitHub repository settings, scrolled to the **GitHub Pages** section, and set the source to the `master` (or `main`) branch. GitHub then automatically built and published the site.

🟢 **Live Portfolio:** [https://danebarnes.github.io](https://danebarnes.github.io)

---

This project demonstrates my ability to use developer tools like **Git**, **Jekyll**, and **GitHub** to build, customize, and deploy a professional website. It’s a testament to my journey in web development and version control, and a window into the kinds of tools and workflows I use daily.
