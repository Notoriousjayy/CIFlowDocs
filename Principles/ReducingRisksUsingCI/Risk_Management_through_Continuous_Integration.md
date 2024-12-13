# **Mitigating Risks with Continuous Integration (CI)**

_"Quality is doing the right thing even when no one is watching."_  
— HENRY FORD  

Projects inevitably encounter obstacles. However, through effective application of Continuous Integration (CI), you can identify and address these challenges at every stage of development, rather than discovering them late in the cycle. CI provides the means to evaluate and report on the health of your project using tangible metrics. Wondering how much of the software is complete? Check the latest build. Curious about the level of test coverage? Check the latest build. Need to know who committed the most recent changes? Check the latest build.

This chapter explores how CI mitigates risks such as late detection of defects, insufficient project visibility, poor software quality, and challenges in creating deployable software.

Many teams start projects with strong intentions but become overwhelmed by unforeseen problems. Often, these issues stem from inadequate risk management. Teams rarely dismiss practices like testing or code reviews as unimportant, yet these are the first areas sacrificed when under tight deadlines. This chapter delves into how CI reduces software risks, enabling teams to construct a "quality safety net" that supports faster delivery. Each integration builds a foundation for addressing risks promptly and consistently.

**CI Enhances Software Quality and Reduces Risks**  

Reducing risks translates to higher software quality. To discuss these risks, we use a structured approach:  

1. An explanation and overview of the software risk  
2. A real-world scenario demonstrating the impact of the risk  
3. A CI-based solution to address and reduce the risk  

While every project faces a variety of risks, this chapter focuses on the ones that CI can directly mitigate. CI may not resolve business challenges like gathering requirements, understanding industry-specific nuances, securing funding, or managing resources. However, CI excels at uncovering software-related issues early in the development process.

By integrating software continuously, CI shifts the timeline in your favor. It allows teams to focus on broader, more complex project challenges earlier. Since CI incorporates a combination of best practices, the risks discussed here encompass multiple areas of software development, including:  

- Inability to create deployable software  
- Late identification of defects  
- Limited visibility into project progress  
- Low-quality deliverables  

You might think, "These risks are familiar; I already know about them." But awareness alone doesn’t equate to mitigation. CI offers practical, efficient methods to tackle these challenges, ensuring they no longer dominate your projects. The key lies in thoughtful implementation. In later chapters, we’ll demonstrate how using a model like the "Integrate button" can help teams effectively identify and address these risks.

## Risk: Lack of Deployable Software

On one project, we only built the software once every few weeks, using a dedicated machine. When the build finally happened—usually right before a delivery deadline—the team often worked late into the night to resolve last-minute issues in what became known as "integration hell." During this chaotic process, we discovered broken interfaces, missing configuration files, redundant components performing similar functions, and difficulties merging numerous changes. These problems frequently caused delays, preventing us from meeting critical milestones.

In another project, software integration was handled manually through an IDE. The process occurred weekly and involved using custom scripts, some of which weren’t even stored in the version control system. Without proper automation or a clean build environment, confidence in the builds was low. The resulting challenges were:

- A lack of confidence in the ability to create reliable builds  
- Lengthy integration cycles that delayed other work  
- Difficulty producing and reproducing testable builds  

#### Scenario: “It Works on My Machine”

A common problem arises when software behaves differently across environments. Here's one example:

**John (Technical Lead):** We’re seeing issues with the latest build on the test server.  
**Adam (Developer):** That’s strange—it works fine on my machine. Let me check... Yep, still works here.  
**John:** Oh, I see. You forgot to commit your updated files to the Git repository.  

#### Solution

To avoid these issues, it’s crucial to decouple the build process from the IDE and use a dedicated machine for integration. All artifacts required to build the software must be in version control. Additionally, automate the build process using tools like Maven or CMake. Pair these tools with a CI server such as Jenkins to automate builds, tests, inspections, and deployments.

Jenkins monitors the Git repository for changes and triggers the build script whenever updates are detected. This ensures the latest software is always integrated and ready for testing or deployment in development and test environments. With this setup, you minimize errors and maintain a deployable software state.


#### Scenario: Database Synchronization Issues

Development can grind to a halt if the database isn’t synchronized with the codebase. This often happens when there’s limited collaboration between the database and development teams. For example, the database administrator might fail to commit critical database scripts to version control, leading to the following problems:

- Hesitation to refactor the database or source code  
- Difficulty generating test data  
- Challenges maintaining consistent development and test environments  

Here’s a common dialogue illustrating this issue:  

**Lauren (Developer):** I’m testing with build 1345, but I’m running into issues using database version v1.2.1.b1.  
**Pauline (Database Designer):** Oh, you need v1.2.1.b2 for that build, but I still need to make some changes to it.  
**Lauren:** Great, I just wasted four hours testing the wrong setup.  
**Pauline:** You should have checked with me first.  

#### Solution

Treat the database as part of the development process by placing all database artifacts—including schema creation scripts, stored procedures, triggers, and test data—in version control. Automate the database setup in your build script to ensure the database is consistently recreated, updated, and populated with test data during each build. Use component tests to validate the database and its contents.  


#### Scenario: Manual Deployment Bottlenecks

Manual deployment often leads to inefficiencies and errors. On one project, we deployed software using an application server’s web interface. This manual process took 10–15 minutes daily and was prone to mistakes—such as forgetting to select specific deployment options. This inefficiency created delays, as illustrated below:

**Rachel (Developer):** Is the latest build deployed on the development server? Where’s John?  
**Kelly (Developer):** He’s at lunch. He was supposed to handle it.  
*Later...*  
**Rachel:** John, the JSPs weren’t precompiled, so we’re seeing runtime errors.  
**John (Technical Lead):** Oops, I forgot to enable that option when deploying yesterday.  

#### Solution

Automate the deployment process by adding deployment tasks to your Maven or CMake build scripts. Use the application server’s command-line tools to handle deployments programmatically. Integrate these scripts with Jenkins to automate deployments whenever changes are made to the Git repository. This ensures a reliable, testable version of the software is always available. Automating these steps reduces bottlenecks and eliminates human error.  

By addressing these risks with automated, CI-driven processes, you can ensure deployable, testable software at every stage of development. For more on these practices, see Chapter 8.

## Risk: Late Detection of Defects

In some projects, testing was performed manually, making it difficult to detect when recent changes introduced new issues. This often resulted in the classic problem: fixing one defect only to have others emerge elsewhere in the system. The lack of automated testing left developers uncertain about the downstream impacts of their changes. There was no assurance that tests were consistently run across the software since everything depended on manual effort.


#### Scenario: Regression Testing

Consider a scenario involving regression testing:  

**Sally (Technical Lead):** I noticed the latest version deployed to the test environment has the same bug we encountered two months ago. How did this happen?  
**Kyle (Developer):** I’m not sure—I tested all my recent changes.  
**Sally:** Did you run tests for the other parts of the system?  
**Kyle:** No, I didn’t have time to manually go through all those tests. That’s probably why the bug slipped through before deployment.  


#### Solution  

We tackled this issue by integrating automated unit and component testing into our development workflow. For new projects, we wrote tests at various layers (business, data, and shared logic) using frameworks compatible with our stack, such as Jest for TypeScript or CTest for C/C++. For existing codebases, we created targeted unit tests based on previously reported defects.  

To ensure these tests were continuously executed, we set up Jenkins to integrate with Git. The build pipeline ran all unit tests using tools like Maven for Java or CMake for C/C++, generating reports after every build.  

Steps to enable automated regression testing include:  

1. Write unit tests for your source code (an xUnit framework is an excellent starting point).  
2. Integrate tests into your build pipeline using tools such as Maven or CMake.  
3. Use Jenkins to continuously execute these tests upon every commit to the Git repository.  

With this approach, regression testing becomes seamless and automated. We cover deeper integrations of testing into builds in Chapter 6.


#### Scenario: Test Coverage  

Automating tests is one part of the solution, but ensuring sufficient coverage is another challenge. Here’s an example:  

**Evelyn (Manager):** Did you run unit tests before committing your changes?  
**Noah (Developer):** Yes.  
**Evelyn:** Great. How about the other feature you’re implementing?  

Now consider this improved dialogue:  

**Evelyn:** Did you write or update tests for your changes?  
**Noah:** Yes.  
**Evelyn:** Did all tests pass?  
**Noah:** Yes.  
**Evelyn:** How did you ensure the tests adequately covered your code?  

This line of questioning highlights the need for quantitative metrics rather than relying solely on verbal confirmation.  


#### Solution  

Code coverage tools provide measurable insights into how much of the codebase is exercised by tests. Tools like Istanbul for TypeScript or gcov for C/C++ can report test coverage percentages by module, package, or class.  

Using Jenkins, we automated the execution of these tools as part of our CI pipeline. Every change committed to the Git repository triggered a build that ran the tests and generated coverage reports. This ensured that developers and managers could independently verify that sufficient coverage was maintained.  

By embedding code coverage checks into the CI process, teams can ensure a consistent level of quality and identify untested areas of the codebase. For more on this topic, see Chapter 7.  

## Risk: Lack of Project Visibility

Relying on manual communication methods for project updates often requires significant effort and coordination to ensure the right people receive information promptly. While telling the developer next to you that the latest build is on a shared drive can work in a small setting, it doesn’t scale. What happens if other team members need this information but are away or unavailable? Similarly, sending a manual email to notify everyone of a critical issue might seem like a solution, but it’s prone to human error—someone may be left out, or the intended recipients may not check their email in time.

#### Scenario: “Did You Get the Memo?”  

Here’s an example of how lack of communication can affect progress:  

**Evelyn (Manager):** What are you working on, Noah?  
**Noah (Tester):** I’m waiting for the latest build to be deployed to QA so I can start testing.  
**Evelyn:** The latest build was deployed to the test server two days ago. Didn’t you hear?  
**Noah:** No, I was out of the office for the past few days.  


#### Solution  

To address this challenge, we implemented a Jenkins CI server that sends automated notifications to all relevant team members whenever a build is completed or fails. Notifications are sent via email and SMS to ensure timely delivery, even if team members are away from their desks. Additionally, automated monitoring agents were configured to regularly check server availability and alert the team if issues arose.  

This system significantly reduced communication overhead while ensuring everyone stayed informed about critical updates in real time.  


#### Scenario: Inability to Visualize Software  

In another instance, the team was tasked with enhancing and modifying an existing codebase. However, they struggled due to the absence of a high-level overview or visual representation of the software’s design. Without up-to-date class diagrams or architectural models, understanding the relationships between components was slow and error-prone.  

**Maile (Developer):** Hi, I’m new to the project and was wondering if there are any UML or other design diagrams I could review.  
**Allie (Developer):** We don’t bother with UML here. If you want to understand the design, read the code. If that’s a problem, maybe this isn’t the right place for you.  
**Maile:** I can read the code; I was just hoping for a big-picture view of the architecture to understand the overall structure.  


#### Solution  

To improve visibility into the software design, we automated the generation of class diagrams and architectural documentation using Doxygen. The CI pipeline was configured to run Doxygen as part of the Jenkins build process, ensuring that the diagrams were always up-to-date with the latest changes in the Git repository.  

For new team members, we complemented the automated diagrams with a concise architectural overview document. This document highlighted the key components, their relationships, and important interfaces, providing a quick and accessible entry point into the project’s design.  

By integrating these tools into the CI workflow, we ensured that the team had consistent, accurate, and easily accessible visualizations of the software, reducing onboarding time and improving decision-making across the project.  

## Risk: Low-Quality Software

Defects can arise not only from clear issues in code but also from potential problems, such as poor design, inconsistent adherence to project standards, or overly complex, hard-to-maintain structures. These "code smells"—symptoms that something might be wrong—are early warning signs of deeper issues. While some may view low-quality software as merely a deferred cost after delivery, the reality is that it leads to numerous challenges during development. Complex or poorly structured code often results in bugs, missed deadlines, and increased maintenance costs. Identifying and addressing these problems early saves significant time and resources while boosting overall software quality.  


#### Scenario: Coding Standard Adherence  

Here’s a common interaction that highlights the challenge of inconsistent coding practices:  

**Brian (Developer):** It’s hard to understand your code. Did you review the project’s coding standards when you started?  
**Lindsay (Developer):** I’ve been using the style from my previous job. My code is a bit complex, which might make it harder for you to follow.  
**Brian:** Writing incomprehensible code doesn’t make you better; it makes collaboration harder. It’s slowing down code reviews and updates. Please take a look at the coding standards and refactor your code accordingly.  

#### Solution  

Instead of lengthy, rarely referenced coding standards documents, we created a concise, annotated reference file that outlined the essential guidelines. Automated code inspection tools, such as ESLint for TypeScript or cppcheck for C++, were integrated into our CI pipeline using Jenkins. These tools flagged violations during the build process, and any infractions were reported in an HTML summary attached to the Jenkins dashboard.  

To enforce standards, newer projects were configured to fail the build if coding guidelines were violated, ensuring compliance from the start.  

#### Scenario: Architectural Adherence  

Over time, software projects often deviate from their original architecture, leading to maintainability issues. For example, consider a project with an initial guideline: “The data layer must not directly interact with the business layer.” Over time, new developers might bypass this rule for convenience, introducing inconsistencies that undermine the architecture.  

**Jenn (Architect):** I noticed one of the controllers is directly accessing the data layer. That violates our design principles.  
**Mark and Charlie (Developers):** (Confused expressions)  
**Jenn:** Our architectural guidelines have been in place for months. Why aren’t they being followed?  
**Charlie:** The architecture has changed so often that it’s hard to keep up.  

#### Solution  

We incorporated automated tools to analyze adherence to architectural guidelines. For example, dependency analysis tools like SonarQube or JDepend were configured to validate the project structure during each build. These tools generated reports identifying violations, ensuring the team could address them promptly. By integrating these checks into Jenkins, architectural adherence became an integral part of the CI pipeline.  

#### Scenario: Duplicate Code  

Duplicate code makes software harder to maintain and increases the risk of bugs. Copy-pasted or redundant logic is common, leading to inefficiencies and inconsistencies. For example:  

**Mary (Developer):** How can I iterate over a collection of `User` objects?  
**Adam (Developer):** I wrote some code for that last week in the `User` package.  
**Mary:** Great! I’ll copy it into my code. Thanks.  

This duplication compounds over time, making refactoring and maintenance increasingly challenging.  

#### Solution  

To manage this, we employed tools like PMD’s Copy-Paste Detector (CPD) or Simian to identify and report duplicate code. These tools were integrated into the CI pipeline, allowing us to continuously monitor duplication levels.  

Steps to reduce duplication included:  

1. Analyze the codebase with a duplication detector and incorporate it into the build script.  
2. Refactor repeated logic into reusable components or methods.  
3. Continuously run duplication checks through the Jenkins pipeline to track improvement over time.  

This approach not only reduced duplication but also encouraged the creation of modular, maintainable components.  

By leveraging automated tools and incorporating checks into the CI process, low-quality software can be transformed into a well-structured, maintainable system. These practices ensure consistent standards, adherence to architecture, and reduced duplication, resulting in higher-quality outcomes. For more detailed inspections and recommendations, refer to Chapter 7.
