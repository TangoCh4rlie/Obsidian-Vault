- [ ] virtualisation
- [ ] docker
- [ ] build a drone
- [ ] asm
- [ ] linux
- [ ] mistral
- [ ] pipeline github
- [ ] k8s
- [ ] next


Plan

- intro
- explain what is a pipeline and the concept to use it (differences with gitlab)
- Build quickly small app in java and show the desing of the units test (use key or something like that in .env to use secrets in the pipeline).
- build the pipeline and explain it in the same time (explain the test for differents OS and you can use matrix to do that)
- change the code to show when the pipeline is not good
- Show pipeline with more complexity
- conclu


[Opening Scene: Host standing in front of a computer screen with GitHub interface visible]

**Modify the intro**
Host: Hey guys, welcome back to our channel! Today, we're diving into the fascinating world of GitHub workflows and pipelines. You may have heard these terms thrown around, but what exactly are they? Well, stick around because we're about to break it all down for you.

[Cut to Screen Recording: GitHub interface with a repository]

Host (Voiceover): Alright, so let's start with the basics. What is a workflow? In the context of GitHub, a workflow is essentially a set of automated processes that are triggered by various events in your repository. These events could include things like code pushes, pull requests, or even scheduled tasks.

[Cut to Host]

Host: Now, you might be wondering why workflows are important. Well, they can help streamline your development process, automate repetitive tasks, and ensure consistent quality across your projects. This, will save you a ton of time, you can trust me.

[Cut to Screen Recording: GitHub Actions tab]

Host (Voiceover): One of the most powerful tools for creating workflows in GitHub is GitHub Actions. With Actions, you can define custom workflows using YAML files right in your repository.
GitLab have some workflows tools but we will only focus on the GitHub tools.

[Cut to Host]

Host: Alright, let's dive into an example. Say you want to automatically run tests whenever someone opens a pull request. With GitHub Actions, you can create a workflow that triggers whenever a pull request is opened, runs your tests, and reports the results back to you.

(On montre la pipeline finale pour les test avec JUnit, il faudra la refaire en live pour que ce soit plus interractif pour l'utilisateur)

[Cut to Screen Recording: YAML file defining a workflow]

Host (Voiceover): Here's what a basic workflow might look like in YAML format. You define the event triggers, the actions to be taken, and any additional configuration options.


[Cut to Host]

Host: Now, let's talk about pipelines. While workflows are focused on automating tasks within your repository, pipelines take things a step further by orchestrating the entire software delivery process.

[Cut to Screen Recording: Pipeline visualization tool]

Host (Voiceover): Pipelines typically consist of multiple stages, each representing a different phase of the delivery process, such as building, testing, and deploying your code. You can use tools like GitHub Actions or third-party CI/CD platforms to create and manage your pipelines.

[Cut to Host]

Host: So, to sum it all up, workflows and pipelines are essential tools for automating and optimizing your development process on GitHub. Whether you're a solo developer working on a side project or part of a large team shipping code to production, mastering these concepts can take your productivity to the next level.

[Closing Scene: Host wrapping up]

Host: Well, that's it for today's video! We hope you found this introduction to GitHub workflows and pipelines helpful. If you did, don't forget to give this video a thumbs up and subscribe to our channel for more content like this. Thanks for watching, and we'll see you next time!
