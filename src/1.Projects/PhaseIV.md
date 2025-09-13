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
#### **Works cited**

1. Automating Projects using Actions \- GitHub Docs, accessed September 1, 2025, [https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/automating-projects-using-actions](https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/automating-projects-using-actions)  
2. Planning and tracking with Projects \- GitHub Docs, accessed September 1, 2025, [https://docs.github.com/en/issues/planning-and-tracking-with-projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects)  
3. GitHub Issues · Project planning for developers, accessed September 1, 2025, [https://github.com/features/issues](https://github.com/features/issues)  
4. Using GitHub issues to manage my tasks because I got tired of all the markdown files. : r/ClaudeAI \- Reddit, accessed September 1, 2025, [https://www.reddit.com/r/ClaudeAI/comments/1mozlq0/using\_github\_issues\_to\_manage\_my\_tasks\_because\_i/](https://www.reddit.com/r/ClaudeAI/comments/1mozlq0/using_github_issues_to_manage_my_tasks_because_i/)  
5. About Projects \- GitHub Docs, accessed September 1, 2025, [https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects](https://docs.github.com/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)  
6. kamranahmedse/developer-roadmap: Interactive roadmaps, guides and other educational content to help developers grow in their careers. \- GitHub, accessed September 1, 2025, [https://github.com/kamranahmedse/developer-roadmap](https://github.com/kamranahmedse/developer-roadmap)  
7. I saved 10+ of repetitive manual steps using just 4 GitHub Actions workflows \- Reddit, accessed September 1, 2025, [https://www.reddit.com/r/devops/comments/1jbajbr/i\_saved\_10\_of\_repetitive\_manual\_steps\_using\_just/](https://www.reddit.com/r/devops/comments/1jbajbr/i_saved_10_of_repetitive_manual_steps_using_just/)  
8. A personal knowledge management and sharing system for VSCode \- Foam, accessed September 1, 2025, [https://foambubble.github.io/foam/](https://foambubble.github.io/foam/)  
9. foambubble/foam: A personal knowledge management and sharing system for VSCode \- GitHub, accessed September 1, 2025, [https://github.com/foambubble/foam](https://github.com/foambubble/foam)  
10. Foam \- Visual Studio Marketplace, accessed September 1, 2025, [https://marketplace.visualstudio.com/items?itemName=foam.foam-vscode](https://marketplace.visualstudio.com/items?itemName=foam.foam-vscode)  
11. Recommended Extensions | Foam, accessed September 1, 2025, [https://foam-template-gatsby-kb.vercel.app/recommended-extensions](https://foam-template-gatsby-kb.vercel.app/recommended-extensions)  
12. Recommended Extensions \- Foam, accessed September 1, 2025, [https://foambubble.github.io/foam/user/getting-started/recommended-extensions.html](https://foambubble.github.io/foam/user/getting-started/recommended-extensions.html)  
13. Visual Studio Code Extensions \- thecrumb, accessed September 1, 2025, [https://www.thecrumb.com/posts/2022-12-21-my-vscode-extensions/](https://www.thecrumb.com/posts/2022-12-21-my-vscode-extensions/)  
14. Introduction \- mdBook Documentation, accessed September 1, 2025, [https://rust-lang.github.io/mdBook/](https://rust-lang.github.io/mdBook/)  
15. Renderers \- mdBook Documentation \- GitHub Pages, accessed September 1, 2025, [https://rust-lang.github.io/mdBook/format/configuration/renderers.html](https://rust-lang.github.io/mdBook/format/configuration/renderers.html)  
16. Continuous Integration \- mdBook Documentation \- GitHub Pages, accessed September 1, 2025, [https://rust-lang.github.io/mdBook/continuous-integration.html](https://rust-lang.github.io/mdBook/continuous-integration.html)  
17. Creating Your First CI/CD Pipeline Using GitHub Actions | by Brandon Kindred \- Medium, accessed September 1, 2025, [https://brandonkindred.medium.com/creating-your-first-ci-cd-pipeline-using-github-actions-81c668008582](https://brandonkindred.medium.com/creating-your-first-ci-cd-pipeline-using-github-actions-81c668008582)  
18. peaceiris/actions-gh-pages: GitHub Actions for GitHub Pages Deploy static files and publish your site easily. Static-Site-Generators-friendly., accessed September 1, 2025, [https://github.com/peaceiris/actions-gh-pages](https://github.com/peaceiris/actions-gh-pages)  
19. Step by step to publish mdBook in gh-pages · Issue \#1803 \- GitHub, accessed September 1, 2025, [https://github.com/rust-lang/mdBook/issues/1803](https://github.com/rust-lang/mdBook/issues/1803)  
20. How to build mdBook with Github Actions | by katopz | Medium \- Level Up Coding, accessed September 1, 2025, [https://levelup.gitconnected.com/how-to-build-mdbook-with-github-actions-eb9899e55d7e](https://levelup.gitconnected.com/how-to-build-mdbook-with-github-actions-eb9899e55d7e)  
21. Beginner's Guide To Python Automation Scripts (With Code ..., accessed September 1, 2025, [https://zerotomastery.io/blog/python-automation-scripts-beginners-guide/](https://zerotomastery.io/blog/python-automation-scripts-beginners-guide/)  
22. 19 Super-Useful Python Scripts to Automate Your Daily Tasks \- Index.dev, accessed September 1, 2025, [https://www.index.dev/blog/python-automation-scripts](https://www.index.dev/blog/python-automation-scripts)  
23. OpenRouter: A unified interface for LLMs | by Dagang Wei | Medium, accessed September 1, 2025, [https://medium.com/@weidagang/openrouter-a-unified-interface-for-llms-eda4742a8aa4](https://medium.com/@weidagang/openrouter-a-unified-interface-for-llms-eda4742a8aa4)  
24. Community Providers: OpenRouter \- AI SDK, accessed September 1, 2025, [https://ai-sdk.dev/providers/community-providers/openrouter](https://ai-sdk.dev/providers/community-providers/openrouter)  
25. Models \- OpenRouter, accessed September 1, 2025, [https://openrouter.ai/models](https://openrouter.ai/models)  
26. Google AI Studio | Gemini API | Google AI for Developers, accessed September 1, 2025, [https://ai.google.dev/aistudio](https://ai.google.dev/aistudio)  
27. Google AI Studio, accessed September 1, 2025, [https://aistudio.google.com/](https://aistudio.google.com/)  
28. Google AI Studio quickstart \- Gemini API, accessed September 1, 2025, [https://ai.google.dev/gemini-api/docs/ai-studio-quickstart](https://ai.google.dev/gemini-api/docs/ai-studio-quickstart)  
29. Google AI Studio for Beginners \- YouTube, accessed September 1, 2025, [https://www.youtube.com/watch?v=IHOJUJjZbzc](https://www.youtube.com/watch?v=IHOJUJjZbzc)  
30. OpenRouter API Reference | Complete API Documentation ..., accessed September 1, 2025, [https://openrouter.ai/docs/api-reference/overview](https://openrouter.ai/docs/api-reference/overview)  
31. Completion | OpenRouter | Documentation, accessed September 1, 2025, [https://openrouter.ai/docs/api-reference/completion](https://openrouter.ai/docs/api-reference/completion)  
32. Summarizing Text Using Hugging Face's BART Model \- DEV Community, accessed September 1, 2025, [https://dev.to/dm8ry/summarizing-text-using-hugging-faces-bart-model-14p5](https://dev.to/dm8ry/summarizing-text-using-hugging-faces-bart-model-14p5)  
33. How to Build A Text Summarizer Using Huggingface Transformers \- freeCodeCamp, accessed September 1, 2025, [https://www.freecodecamp.org/news/how-to-build-a-text-summarizer-using-huggingface-transformers/](https://www.freecodecamp.org/news/how-to-build-a-text-summarizer-using-huggingface-transformers/)  
34. Pipelines \- Hugging Face, accessed September 1, 2025, [https://huggingface.co/docs/transformers/main\_classes/pipelines](https://huggingface.co/docs/transformers/main_classes/pipelines)  
35. How to Run LLMs Locally with Ollama \- Medium, accessed September 1, 2025, [https://medium.com/cyberark-engineering/how-to-run-llms-locally-with-ollama-cb00fa55d5de](https://medium.com/cyberark-engineering/how-to-run-llms-locally-with-ollama-cb00fa55d5de)  
36. Running LLM Locally: A Beginner's Guide to Using Ollama | by Arun Patidar | Medium, accessed September 1, 2025, [https://medium.com/@arunpatidar26/running-llm-locally-a-beginners-guide-to-using-ollama-8ea296747505](https://medium.com/@arunpatidar26/running-llm-locally-a-beginners-guide-to-using-ollama-8ea296747505)  
37. ollama/ollama: Get up and running with OpenAI gpt-oss ... \- GitHub, accessed September 1, 2025, [https://github.com/ollama/ollama](https://github.com/ollama/ollama)  
38. Learn Ollama in 15 Minutes \- Run LLM Models Locally for FREE \- YouTube, accessed September 1, 2025, [https://www.youtube.com/watch?v=UtSSMs6ObqY](https://www.youtube.com/watch?v=UtSSMs6ObqY)  
39. usememos/memos: A modern, open-source, self-hosted knowledge management and note-taking platform designed for privacy-conscious users and organizations. \- GitHub, accessed September 1, 2025, [https://github.com/usememos/memos](https://github.com/usememos/memos)  
40. siyuan-note/siyuan: A privacy-first, self-hosted, fully open source personal knowledge management software, written in typescript and golang. \- GitHub, accessed September 1, 2025, [https://github.com/siyuan-note/siyuan](https://github.com/siyuan-note/siyuan)  
41. Best Open Source Personal Knowledge ... \- OpenAlternative, accessed September 1, 2025, [https://openalternative.co/categories/personal-knowledge-management-pkm/using/rust](https://openalternative.co/categories/personal-knowledge-management-pkm/using/rust)  
42. Modular: A Fast, Scalable Gen AI Inference Platform, accessed September 1, 2025, [https://www.modular.com/](https://www.modular.com/)  
43. Modular Documentation | Modular, accessed September 1, 2025, [https://docs.modular.com/](https://docs.modular.com/)  
44. Get started with Mojo \- Modular docs, accessed September 1, 2025, [https://docs.modular.com/mojo/manual/get-started/](https://docs.modular.com/mojo/manual/get-started/)  
45. The Modular Platform (includes MAX & Mojo) \- GitHub, accessed September 1, 2025, [https://github.com/modular/modular](https://github.com/modular/modular)