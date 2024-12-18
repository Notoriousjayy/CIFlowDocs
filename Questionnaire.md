# **Getting Started**  
**Questions**  
How do you know you are doing CI correctly? These questions can help you decide what’s missing on your projects.

- Are you using a version control repository (or SCM tool)?  
- Is your project’s build process automated and repeatable? Does it occur entirely without intervention?  
- Are you writing and running automated tests?  
- Is the execution of your tests a part of your build process?  
- How do you enforce coding and design standards?  
- Which of your feedback mechanisms are automated?  
- Are you using a separate integration machine to build software?



# **Introducing Continuous Integration**  
**Questions**  
Practicing CI is more than installing and configuring some tools. How many of the following items are you consistently performing on your project? How many of the other CI practices can improve your development capabilities?

- On average, is everyone on your team committing code at least once a day? Are you employing techniques to make it easier to commit code often?  
- What percentage of each day’s integration builds is successful (that is, the most recent build run has passed)?  
- Is everyone on your team running a private build before committing to the repository so that integration errors are reduced?  
- Have you scripted your builds to fail if any of your tests or inspections fail?  
- Is a broken integration build a priority to fix on your projects?  
- Do you avoid getting the latest code from the version control system when there is a broken build?  
- How often do you consider adding automated processes to your build and CI system—on a continuous or even periodic basis?



# **Reducing Risks Using CI**  
**Questions**  
How many risks do you have on your project that CI can help mitigate? These questions should help you determine the risks on your project.

- When do you find the most defects on your project, in the beginning or in later parts of the lifecycle?  
- How do you determine the quality on your software projects? Are you able to measure it?  
- Which processes on your projects are manual? Have you determined which processes you can or should automate?  
- Do you have all of the scripts to rebuild your database and data in your version control repository? Are you able to rebuild your database and test data during the build process?  
- Are you able to perform regression testing whenever a change is made to the software? Are you able to run various types of regression tests, including functional, integration, load, and performance tests?  
- Do you have the capability to determine which source code does not have a corresponding test? Are you using test coverage tools?  
- What percentage of your software has duplicate code? Are you seeking to reduce this amount?  
- At any point in time, how do you verify that the current source code adheres to the software architecture?  
- How do you notify that the build or deployment is ready to test? Which communication mechanisms on your project are manual, and which should be automated?  
- Are you able to view a current visual diagram of your software? How do you communicate the software architecture to a new developer on the project?



# **Building Software at Every Change**  
**Questions**

- Is your build automated? Are you able to run your build without your IDE?  
- Have you centralized all of your software assets into your version control repository? Are you able to perform a complete build by getting all necessary files from the version control repository?  
- Do you ensure that the build tasks that are more likely to fail are at the beginning of your build scripts so that you receive notification of a build failure quickly?  
- Do you have an “Integrate button” for your software build processes? Is your database integration automated? Testing? Inspection? Deployment? Are you receiving and using feedback from the process?  
- Does your integration build process occur on a separate machine?  
- What is the duration of your integration builds? Are you seeking to shorten your build duration to improve feedback?  
- Are you using a CI server to integrate your software? Or do you have a disciplined process for manually integrating builds?  
- How often does your project perform integration builds: weekly, nightly, or hourly? Or is it at every change (continuously)?



# **Continuous Database Integration**  
**Questions**  
These questions can help you determine your level of automation and continuous database integration.

- Are you capable of recreating your database from your automated build process? Can you rebuild your database at the “push of a button?”  
- Are the scripts (build and SQL) to your database integration automation committed to your version control repository?  
- Is everyone on your project capable of recreating the database using the automated build process?  
- During development, are you able to go back to prior versions of the database using your version control repository?  
- Is your database integration process continuous? Are your software code changes integrated and tested with the latest database whenever you apply those changes to the version control repository?  
- Are you running tests to verify the behavior of your database stored procedures and triggers?  
- Is your automated database integration process configurable? Are you able to modify the userid, password, unique database identifier, tablespace size, and so on using a single configuration file?



# **Continuous Testing**  
**Questions**  
Use this list of questions to evaluate your test process in light of the CI environment and what it can provide for you.

- Are you categorizing your automated tests, such as unit tests, component tests, system tests, and functional tests?  
- Are you configuring your CI system to run each test category with different staged builds?  
- Are you writing automated unit tests for each defect?  
- How many asserts are in each of your test cases? Are you limiting each test case to one assert?  
- Are these tests automatable? Has your project committed automated developer tests to the version control repository?



# **Continuous Inspection**  
**Questions**  
The following questions will help you devise your own continuous inspection process.

- Do you perform unit testing sporadically, periodically, or continuously? How often do you run your full unit, component, and system test coverage review?  
- Are you monitoring code complexity?  
- Are you continuously performing automated design reviews with tools like JDepend and NDepend?  
- Are you automating code audits with tools like PMD, Checkstyle, or FxCop?  
- Are you monitoring code duplication?  
- Are you able to assess code coverage? How are you reacting to the data?  
- Do you know what percentage of your code has a corresponding test?  
- Is your build properly configured to produce coverage reports?



# **Continuous Deployment**  
**Questions**  
Are your deployments automated? How quickly are you able to get a release out into production? How quickly are you able to get the software into your development or test environment? Use these questions to determine your project’s capability to continuously deploy software.

- Do you possess the capability to roll back a release?  
- Are you labeling your builds in your version control system?  
- Do you have a full set of automated tests that are followed by manual tests of the release candidate afterward?  
- How does your team handle release fixes?  
- Are your version control labels and build versions related?  
- Does your build produce feedback reports?  
- Are you able to deploy your software from the command line with a single command?  
- Are you building your deployments from the version control repository?  
- Are you able to configure your deployments for different environments? Does your software install and run properly on a “clean” machine clone of the user’s environment?  
- Do you have a bug tracking system, and can it generate reports?



# **Continuous Feedback**  
**Questions**  
Here is a handy list of considerations to help you develop continuous feedback mechanisms in your development environment.

- Have you automated your feedback processes?  
- Is your feedback incorporated into your CI system so that feedback does not need to be sent manually?  
- Are the right people getting notified? Are too many people being notified too often?  
- Is the feedback timely? Are project members receiving the feedback as soon as a problem is identified?  
- Are you sending the appropriate amount of information to project members?  
- Is your team distributed geographically? Are you automating your information radiators?  
- Are you making feedback fun? Have you incorporated devices such as sounds or the Ambient Orb into your feedback processes?



**Categorization:**

- **Getting Started** – Questions focus on basic CI setup: version control usage, automated builds, automated tests, coding standards, feedback mechanisms, and integration machines.
- **Introducing Continuous Integration** – Questions focus on the frequency of commits, success rates of builds, private builds, scripted failures, and continuous improvement of CI practices.
- **Reducing Risks Using CI** – Questions focus on identifying defects early, measuring quality, automating processes, rebuilding databases, performing regression tests, ensuring test coverage, reducing duplicate code, and verifying adherence to architecture.
- **Building Software at Every Change** – Questions emphasize automated builds, centralizing assets in version control, quick fail of builds, integration buttons, CI servers, and frequency of integration builds.
- **Continuous Database Integration** – Questions cover the ability to recreate databases automatically, version controlling database scripts, continuous database integration, and testing database procedures.
- **Continuous Testing** – Questions address test categorization, integration with CI, writing automated tests for defects, test granularity (one assert per test), and committing tests to version control.
- **Continuous Inspection** – Questions focus on performing testing (unit, component, system) continuously, monitoring code complexity, automating design reviews, code audits, code duplication monitoring, coverage assessment, and ensuring coverage reports.
- **Continuous Deployment** – Questions revolve around automated deployments, rollback capabilities, labeling builds, combining automated and manual tests, relationship between version control labels and build versions, command-line deployments, configuring environments, and bug tracking.
- **Continuous Feedback** – Questions address automating feedback processes, ensuring timely and appropriate notifications, geographic distribution of teams, and making feedback visible and engaging.
