## **Phase IV: Hyper-Automation and Advanced Workflows (Modules 61-80)**

*Focus: Creating proactive, fully automated pipelines that require minimal manual intervention. This phase builds the "intelligent nervous system" of the PKM.*

### **Modules 61-70: Advanced GitHub Actions Workflows**

This section focuses on creating a sophisticated, multi-stage GitHub Action that fully automates the process of content enrichment, connecting the file system, Python scripts, AI models, and the deployment pipeline.

61. **Designing the "Content Enrichment" Workflow:** A new, more advanced GitHub Actions workflow will be designed. The goal is to create a system that automatically processes a new note, enriches it with AI-generated content, and deploys the result without any manual steps.  
62. **Triggering Workflows with Path Filters and Tags:** The workflow will be configured to trigger conditionally. It will run on pushes to the main branch but only when files in the /notes directory are modified. A convention will be established where adding a specific tag, like \#summarize, to a note's frontmatter signals the workflow to process that specific file.  
63. **Workflow Step: Identifying Target Files:** The first step in the Action's job will be to identify which files have been changed in the latest commit and need processing. A simple shell script or a dedicated GitHub Action can be used to get the list of modified files.  
64. **Workflow Step: Running the AI Python Script:** The workflow will then set up the Python environment and run the AIManager script developed in Phase III. The script will be called with the path to the modified file as an argument.  
65. **Workflow Step: Committing Changes Back to the Repository:** After the Python script runs and modifies the note file (e.g., by adding a summary), the GitHub Action must commit this change back to the repository. This requires configuring Git within the action, setting a user and email, and using git commit and git push. A special commit message like "chore(AI): Add summary to \[filename\]" will be used to denote automated changes.  
66. **Handling Recursive Workflow Triggers:** A critical challenge in this setup is that the workflow pushes a commit, which would normally trigger the workflow again, creating an infinite loop. This will be prevented by adding a condition to the commit step or the workflow trigger to ignore commits made by the Actions bot itself (e.g., by checking the commit message).  
67. **Chaining Workflows:** Instead of putting everything in one massive file, the content enrichment workflow will be configured to trigger the existing mdBook deployment workflow upon its successful completion. This can be done using the workflow\_run event or by using a reusable "callable" workflow, which is a more modern approach.  
68. **Adding an Issue Commenting Step:** To provide feedback, a final step will be added to the workflow. Using an action like peter-evans/create-or-update-comment, the workflow will find the corresponding GitHub Issue for the topic and post a comment indicating that the note has been automatically updated and a new version has been deployed, including a link to the published page.  
69. **Full End-to-End Test:** A full test of the pipeline will be conducted. A new note will be created locally, tagged for summarization, and pushed to GitHub. The process will be monitored in the GitHub Actions tab, from the initial trigger to the AI processing, the commit back, the mdBook deployment, and the final comment on the issue.  
70. **Refactoring for Reusability:** The workflow will be refactored to make it more modular. The Python script execution and the mdBook deployment steps will be broken into separate, reusable composite actions or callable workflows, making the main workflow file cleaner and easier to maintain.7

### **Modules 71-75: Local LLMs with Ollama**

This section introduces local large language models using Ollama, adding a powerful, private, and cost-effective tier to the AI strategy.35

71. **Installing and Configuring Ollama:** Ollama will be installed on the local machine. The command-line interface will be used to pull down a versatile, medium-sized model like Llama 3 (ollama pull llama3) or a smaller, efficient model like Phi-2 (ollama pull phi-2).35  
72. **Interacting with Local Models via CLI and API:** The first interactions will be through the command line using ollama run llama3. This provides a feel for the model's performance and personality. Subsequently, the Ollama REST API, which runs locally on port 11434, will be explored. A tool like curl or Postman will be used to send requests to the API, demonstrating how to interact with the local model programmatically.36  
73. **Creating a Custom Model with a Modelfile:** To tailor a model for specific PKM tasks, a Modelfile will be created.37 This file defines a custom model based on a parent model (e.g.,  
    FROM llama3). It will include a SYSTEM prompt to give the model a specific persona, such as a "Socratic Inquisitor" whose role is to respond to any text by generating three probing questions to deepen understanding. Parameters like temperature can also be set to control creativity.38  
74. **Building and Running the Custom Model:** The ollama create command will be used to build the custom model from the Modelfile, giving it a unique name (e.g., socratic-inquisitor). This new model will then be available to run via ollama run socratic-inquisitor and through the API.37  
75. **Integrating Ollama into the Python AI Toolkit:** The AIManager Python module will be updated to include Ollama as a new AI provider. A new function will be added that makes API calls to the local Ollama server. The routing logic will be updated to use the local model for specific tasks, such as brainstorming or generating questions, officially adding the "Tier 1 (Local)" capability to the system.36

### **Modules 76-80: Containerization with Docker**

To ensure the PKM system's environment is consistent, portable, and reproducible, this section introduces containerization using Docker. This brings professional DevOps practices to the personal project.

76. **Introduction to Docker Concepts:** The core concepts of Docker will be reviewed: images, containers, Dockerfiles, and volumes. The benefits of containerization for creating isolated and predictable environments will be discussed.  
77. **Running Ollama in a Docker Container:** As a first practical step, instead of running Ollama directly on the host machine, it will be run inside a Docker container using the official ollama/ollama image.35 This involves running the container, mapping the necessary ports, and using a volume to persist the downloaded models, ensuring they are not lost when the container stops.  
78. Writing a Dockerfile for the Python Scripts: A Dockerfile will be written for the PKM's Python automation tools. This file will define a custom image that:  
    a. Starts from a base Python image.  
    b. Copies the requirements.txt file and installs the dependencies.  
    c. Copies the /scripts directory into the image.  
    d. Sets up any necessary environment variables.  
79. **Building and Running the Custom Python Container:** The docker build command will be used to create an image from the Dockerfile. Then, docker run will be used to start a container from this image and execute one of the automation scripts, demonstrating that the entire toolchain can run in a self-contained environment.  
80. **Exploring Other Self-Hosted PKM Tools:** Docker makes it easy to experiment with other open-source tools. This module involves exploring the Docker images for other self-hosted PKM platforms like Memos or Siyuan.39 By running these tools locally in containers, new ideas and features can be discovered and potentially incorporated into the custom PKM system, all without polluting the host machine with new dependencies.

---
