## **Phase I: Foundations and Environment Setup (Days 1-20)**

This [initial phase](https://github.com/orgs/AncientGuy/projects/1/views/4) is dedicated to constructing a robust "mission control" for the entire 100-day project. The objective is to establish a fully automated, version-controlled, and meticulously structured environment before commencing any significant feature development. This front-loading of infrastructure work is a critical investment that ensures stability and efficiency over the long term. A key principle of this phase is to apply the tools of the project *to* the project itself, creating a virtuous cycle of learning and practical application from the very first day.

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