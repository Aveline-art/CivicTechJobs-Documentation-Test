# Developer Workflow Cycle

At CivicTechJobs, the developers of our team have 3 key tasks:

- Make issues
- Resolve issues
- Review code

This guide will discuss how each of these work at CivicTechJobs.

## Make Issues

> To make an issue, follow [this guide](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue) from GitHub, or take a look at [this section](https://github.com/hackforla/CivicTechJobs/blob/main/CONTRIBUTING.md#making-issues-1) of the CONTRIBUTING.md.

At CivicTechJobs, updating the project starts with creating an issue noting changes that needs to be made. When writing an issue, a good rule of thumb is to write as if another developer would be the one to work on this issue. Therefore, being thorough is better than brief. Some good guidelines to follow:

- Write a brief, two sentence summary for the overview. Be sure to note why these changes is needed.
- In the overview, use language with little jargon.
- Action items are usually step by step instructions or requirements.
- Longer explanations or useful documentation, if needed, are placed in the Instruction/Resources section.
- Dependencies should 90% of the time be another issue. If the dependency does not exist, it should probably be made and referenced as a dependency.
- Likewise, the dependency should reference the issue it is a dependency for so that there is a trail to release issues with dependencies.
- Check out examples of developer issues, such as [this](https://github.com/hackforla/CivicTechJobs/issues/61), for how to structure and word issues.

After writing out the issue, be sure to [add labels to the issue](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels#applying-a-label). At minimum we need three labels, one each from the "size", "role" and "feature/p-feature" series. In most cases, you should not create your own label. If you cannot choose a label, it is okay to leave it be, and request the project management team to create a new label for you.

Once an issue is created, and placed in the [Project Management](https://github.com/hackforla/CivicTechJobs/projects/1) project board, the developer is mostly done with the issue. If the issue contains a dependency, it will move into the "Ice Box" column via [GitHub automation](https://github.com/hackforla/CivicTechJobs/blob/bafc2fc1706ac49ec9c2c7cb610a29bddc561339/.github/workflows/issue-trigger.yml#L7), or "New Issue Approval", otherwise.

On rare occasions, a project manager, or other team members, might ping you with questions on the issue. Perhaps the team member did not understand the jargon, or instructions were unclear. In that case, read their comments carefully and either answer them in a comment, or edit the original issue. Eventually, the project management team will be able to correctly assess the priority of the issue and release it into the "Prioritized Backlog" column, where developers can work on it.

## Resolve Issues

> To resolve an issue, take a look at [this section](https://github.com/hackforla/CivicTechJobs/blob/main/CONTRIBUTING.md#resolving-issues-1) of the CONTRIBUTING.md.

When choosing an issue to work on from the "Prioritized Backlog" column, it is good to notice the role and size. This will signal to you the expertise required and time commitment, respectively. As a rule of thumb, every developer should complete a smaller issue withinin a week and larger issues within two or three. This should give you a good idea on what issues is best for you to take at the moment. If you are completely new, we do recommend smaller issues just to understand your limits before pushing them further. That said, you are free to take whatever you want.

On occasion, when an issue is being worked on for an inordiante amount of time, the team might request an update on your progress. When giving your progress, it is also courteous to give an ETA on the issue, and evaluate on whether you have the time availibilty and expertise to deliver in a reasonable timeframe. If an issue is taking far too long, it might be a sign to abandon the issue and work on something that might bring more value to you.

Most issues can be divided into two broad types: frontend issues, and backend issues.

Frontend issues:
- Usually involves the appearence of the website
- Usually easier than backend issues
- Requires little research
- Is occasionally an audit
- May involve documentation

When working on frontend issues, there will usually be a link to the Figma design. Figma often contain multiple prototypes and future prototypes. When looking for our current design, go to the bottom right corner and look for a pink rectangle. Anything within represents our most up-to-date design, and that is the page you must reference when working on your issue. If it is not there, please request the UI design team to put a pink rectangle on the latest approved design.

Very rarely, designs can change in the middle of work. Designers never does this intentially; they require sign off before changing designs. This is a part of development, but the good news is that you will often be aware of upcoming changes during our meetings and can adjust accordingly. You are free to abandon your current issue, or code pragmatically according to the tea leaves.

Backend issues:
- Usually involves research and discussion
- Can also pertain to [GitHub Actions](https://docs.github.com/en/actions)
- Usually takes some time
- May involve documentation

## Review Code

> To review code, please take a look at this [GitHub documentation](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/about-pull-request-reviews), and this portion of our [CONTRIBUTING.md](https://github.com/hackforla/CivicTechJobs/blob/main/CONTRIBUTING.md#reviewing-code).

Code that should be reviewed is found in the [pull request tab](https://github.com/hackforla/CivicTechJobs/pulls). These are issues that require someone to look over for several criteria:

- Applicability: Were the correct changed made? Is the code in the source code only changed to resolve the issue, and nothing else extraneous?
- Brokenness: Did the changes break the website?
- Cleanliness: Is the new code programatic or messy? If it is hard to maintain in the long run, it should not be merged unless it is highly critical.

When code meets all three criteria, it can then be merged and made a part of the website. Otherwise, the review should indicate changes that needs to be made.

As an advanced project, CivicTechJobs have certain expectations for our developers. One of these is that issues of size 1 or 2 is small enough that we pre-review them. What this means is that we believe these issues are too small for a developer to. colloquially speaking, screw it up. These issues can be merged directly without a review from another developer. That said, it is still fine to request the team to review these issues, if you truly desire feedback.

**Important:** Although issues can be pre-reviewed, do not make a habit of merging directly without making a pull request. There will be times when you performed an accidential merge, which could be a pain to fix.

As one final note, code can be merged solely on one review as our team is small, but as with pre-reviewed pull requests, it is fine to request another pair of eyes.