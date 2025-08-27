**Introduction**

Continuous Integration and Continuous Deployment (CI/CD) are critical
practices in modern software development, enabling teams to deliver
high-quality software quickly and efficiently. CI/CD pipelines automate
the process of building, testing, and deploying code, ensuring that
every change is thoroughly tested before being released. GitHub Actions,
GitHub\'s built-in CI/CD tool, offers a simple yet powerful way to
automate these workflows directly from your GitHub repository. This
guide will walk you through setting up your first CI/CD pipeline using
GitHub Actions, which is perfect for beginners.

**What is GitHub Actions?**

GitHub Actions is a feature within GitHub that allows you to automate
tasks directly from your repository. You can create workflows that are
triggered by specific events, such as a push to a branch, a pull
request, or a scheduled time. These workflows can be used to build,
test, and deploy your code and automate other tasks like linting,
security scanning, or releasing software.

**Why Use GitHub Actions?**

1.  **Integration with GitHub:** Seamlessly integrates with your GitHub
    repositories, making it easy to automate workflows without leaving
    the platform.

2.  **Customizable Workflows:** You can create highly customized
    workflows to fit your project's needs using YAML configuration
    files.

3.  **Community-Driven:** Access thousands of pre-built actions and
    workflows from the GitHub Marketplace to speed up your development
    process.

4.  **Scalability:** GitHub Actions can scale with your project,
    supporting simple scripts to complex multi-step pipelines.

**Prerequisites to using GitHub Actions**

Before setting up your first CI/CD pipeline, you\'ll need:

\- A GitHub account

\- A repository to work with (create one if you don't have it)

\- Basic understanding of Git and GitHub

**Step 1: Setting Up Your GitHub Repository**

1\. **Create a New Repository:**

-   Give your repository a name, and description, and choose whether it
    > should be public or private.

-   Click \"Create repository.\"

2\. **Clone the Repository Locally:**

-   Clone your new repository to your local machine using Git.

git clone https://github.com/your-username/your-repository.git

cd your-repository

3\. **Add Your Project Files:**

-   If you already have a project, add the files to this repository. If
    > not, create a simple project to test your CI/CD pipeline. For
    > example, a simple Python project with a \`main.py\` file.

> \# main.py
>
> def hello\_world():
>
> return \"Hello, World!\"
>
> if \_\_name\_\_ == \"\_\_main\_\_\":
>
> print(hello\_world())

4\. **Commit and Push Changes:**

-   Stage, commit, and push your project files to GitHub.

> git add .
>
> git commit -m \"Initial commit\"
>
> git push origin main

**Step 2: Creating Your First GitHub Action Script**

GitHub Actions uses YAML files to define workflows. These files are
stored in the \`.github/workflows/\` directory within your repository.

1.  **Create the Workflow Directory**:

\- In the root of your project, create a new directory called
\`.github/workflows\`.

mkdir -p .github/workflows

**2.** **Create a New Workflow File:**

\- Inside the \`workflows\` directory, create a new file named
\`ci.yml\`.

touch .github/workflows/ci.yml

**3.** **Define the Workflow:**

\- Open the \`ci.yml\` file in a text editor and define your first
workflow.

> name: CI Pipeline
>
> on:
>
> push:
>
> branches:
>
> \- main
>
> pull\_request:
>
> branches:
>
> \- main
>
> jobs:
>
> build:
>
> runs-on: ubuntu-latest
>
> steps:
>
> \- name: Checkout code
>
> uses: actions/checkout\@v3
>
> \- name: Set up Python
>
> uses: actions/setup-python\@v4
>
> with:
>
> python-version: 3.8
>
> \- name: Install dependencies
>
> run: \|
>
> python -m pip install \--upgrade pip
>
> if \[ -f requirements.txt \]; then pip install -r requirements.txt; fi
>
> \- name: Run tests
>
> run: \|
>
> pytest

**Breakdown of the YAML Workflow**

-   name: The name of your workflow, which will appear in the GitHub
    > Actions tab.

-   on: Specifies the events that trigger the workflow. Here, it
    > triggers pushes and pulls requests to the \`main\` branch.

-   jobs: Defines the jobs that will run as part of the workflow.

-   build: The name of the job.

-   runs-on: Specifies the environment the job will run in. Here, we\'re
    > using \`ubuntu-latest\`.

-   steps: Defines the steps within the job.

-   Checkout code: Uses the \`actions/checkout\` action to pull the
    > latest code from the repository.

```{=html}
<!-- -->
```
-   Set up Python: Uses the \`actions/setup-python\` action to set up a
    > Python environment.

-   Install dependencies: Installs the dependencies listed in
    > \`requirements.txt\` (if it exists).

-   Run tests: Run the tests using \`pytest\`.

**Step 3: Running Your Workflow**

Once you commit and push the \`ci.yml\` file to your repository, GitHub
Actions automatically triggers the workflow whenever you push changes or
open a pull request on the \`main\` branch.

1\. **Commit and Push the Workflow File:**

> git add .github/workflows/ci.yml
>
> git commit -m \"Add CI pipeline\"
>
> git push origin main

2\. **View the Workflow:**

-   Navigate to your repository on GitHub.

-   Click on the \"Actions\" tab. You should see the \"CI Pipeline\"
    > workflow listed.

-   Click on the workflow to view the details of the running or
    > completed jobs.

**3. Review the Results:**

-   If everything is set up correctly, you should see each step in your
    > workflow run successfully.

-   Any errors in the pipeline will be displayed, allowing you to debug
    > and make necessary changes.

**Step 4: Expanding Your Pipeline**

Now that you have a basic CI/CD pipeline, you can expand it to include
more steps, such as deployment to AWS or Heroku, linting, notifications,
etc.

**Example:** Deploying to Heroku

You can add deployment steps to your workflow to automatically deploy
your code after passing all tests.

1.  **Add Deployment Step:**

-   name: Deploy to Heroku

> uses: akhileshns/heroku-deploy\@v3.12.12
>
> with:
>
> heroku\_api\_key: \${{secrets.HEROKU\_API\_KEY}}
>
> heroku\_app\_name: \"your-app-name\"
>
> heroku\_email: \"your-email\@example.com\"

2.  **Set Up GitHub Secrets:**

    -   Go to your repository settings and add \`HEROKU\_API\_KEY\` as a
        secret with your Heroku API key.

**Best Practices for CI/CD with GitHub Actions**

1.  **Keep Workflows Simple:** Start with simple workflows and gradually
    add complexity as your project grows.

2.  **Use Secrets for Sensitive Data:** Store API keys and sensitive
    data in GitHub Secrets to keep them secure.

3.  **Test Locally:** Test your scripts and commands locally before
    adding them to your GitHub Actions workflow.

4.  **Monitor Workflow Performance:** Regularly monitor your workflows
    to ensure they run efficiently and make adjustments as needed.

5.  **Leverage the Marketplace:** Explore the GitHub Actions Marketplace
    for pre-built actions to save time and effort.

**Conclusion**

Setting up your first CI/CD pipeline with GitHub Actions is a
significant milestone in your journey as a developer. By automating the
testing and deployment of your code, you can ensure higher code quality
and faster delivery. As you gain more experience, you can expand your
pipelines to include more advanced features and integrations, fully
embracing the power of CI/CD.
