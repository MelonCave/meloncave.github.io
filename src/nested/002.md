## **Phase I: Foundations and Environment Setup (Days 1-20)**

This initial phase is dedicated to constructing a robust "mission control" for the entire 100-day project. The objective is to establish a fully automated, version-controlled, and meticulously structured environment before commencing any significant feature development. This front-loading of infrastructure work is a critical investment that ensures stability and efficiency over the long term. A key principle of this phase is to apply the tools of the project *to* the project itself, creating a virtuous cycle of learning and practical application from the very first day.

### **Week 1: Project Scaffolding (Modules 1-7)**

The first week focuses on creating the digital skeleton of the project. This involves initializing the code repository, setting up the project management tools, and performing an initial manual deployment to understand the end-to-end process.

#### **Modules 1-2: GitHub Repository and Project Initialization**

The foundation begins with a new GitHub repository. To accelerate the setup of the PKM's structure, the project will be bootstrapped using the foam-template.7 This template provides a pre-configured VS Code workspace with recommended extensions (

.vscode/extensions.json) and settings (.vscode/settings.json) optimized for knowledge management tasks, such as Markdown All In One and Prettier.28 Within this repository, a new

mdBook project will be initialized in a dedicated /book subdirectory, creating the initial src directory and SUMMARY.md file that will house the PKM content.6

#### **Modules 3-5: Mission Control with GitHub Projects**

To effectively manage a 100-day endeavor, this entire plan will be translated into a functional project board using GitHub Projects. This approach makes the project plan itself a dynamic, version-controlled artifact. A new GitHub Project will be created, and an issue will be opened for each of the 100 modules. These issues will be organized into phases and categorized using custom fields to track status (e.g., To Do, In Progress, Done), module type (e.g., Setup, Rust, Python, Exploration), and estimated complexity. This immediate application of GitHub Projects transforms project management from a peripheral task into a core component of the learning experience.

#### **Modules 6-7: First Deployment \- Manual CI/CD**

Before automating the deployment process, it is crucial to understand the underlying mechanics. This module involves a manual deployment of the nascent mdBook to GitHub Pages. The repository settings will be configured to deploy from a specific branch, typically gh-pages. The mdbook build command will be run locally to generate the static site in the book/book directory. The contents of this output directory will then be manually committed and pushed to the gh-pages branch. This exercise provides a clear baseline understanding of the build artifacts and the deployment mechanism that will be automated in a later phase.11

### **Week 2: Agent Installation and First Contact (Modules 8-14)**

With the project structure in place, the second week is dedicated to installing, configuring, and establishing a working relationship with the core agentic assistant, Cline.

#### **Modules 8-10: Installing and Configuring Cline**

The primary tool for this project, the Cline VS Code extension, will be installed from the marketplace.4 Configuration is the next critical step. An API key from OpenRouter will be generated and added to the Cline settings.5 OpenRouter serves as a powerful API gateway, providing access to a multitude of LLMs from various providers like Anthropic, Google, and OpenAI.18 Initial experiments will be conducted using different models, such as the powerful

anthropic/claude-3.5-sonnet for complex tasks and the free-tier google/gemini-2.0-flash-exp:free for simpler operations, to gain an intuitive understanding of the cost-performance trade-offs inherent in different models.5

#### **Modules 11-14: Mastering Cline's Core Interactions**

Effective use of an agentic assistant requires learning its interaction patterns. This period will be spent practicing fundamental tasks. Simple, declarative prompts will be used, such as: "Create a new file named TODO.md and add three items," or "Read the README.md file and provide a one-paragraph summary." A crucial distinction to master is the difference between Cline's two primary modes: "Plan" mode, which allows for read-only exploration and task decomposition, and "Act" mode, which executes the proposed changes.33 The "Auto-approve" settings will be explored to understand the balance between the rapid, fluid experience of "vibe coding" and the safety and control of manually approving each step.33 Finally, Cline's ability to interact with the integrated terminal will be tested by instructing it to run commands like

ls \-R to recursively list the project's file structure, confirming its ability to observe and interact with its environment.4

### **Week 3: Full Automation with GitHub Actions (Modules 15-20)**

The final week of the foundational phase focuses on automating the entire build and deployment pipeline, transitioning from the manual process established in Week 1 to a fully autonomous CI/CD workflow. This task itself will be delegated to the agent, serving as a perfect, self-contained test of its capabilities.

#### **Modules 15-20: Building the CI/CD Pipeline**

Instead of manually authoring a YAML configuration file, a high-level, declarative prompt will be given to Cline. For example: "Create a GitHub Actions workflow file at .github/workflows/deploy.yml. This workflow must trigger on every push to the main branch. It should set up a Rust environment, install a specific version of mdBook, execute the mdbook build command, and then use the peaceiris/actions-gh-pages action to deploy the contents of the ./book/book output directory to the gh-pages branch."

This approach forces a shift in thinking from syntactic detail to strategic intent. Cline will generate a plan and the corresponding YAML file for review and approval.12 Once the generated workflow file is committed and pushed to the

main branch, the GitHub Actions runner will be triggered. The successful execution of this workflow will confirm that the site is now being built and deployed automatically. Any errors encountered in the runner's logs will be fed back to Cline for troubleshooting, further simulating a real-world human-AI collaborative debugging session. As a final step, the output.html.site-url setting in book.toml will be configured to ensure that the auto-generated 404 page links correctly within the GitHub Pages environment.11
