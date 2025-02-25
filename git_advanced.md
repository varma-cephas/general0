### Git Branching Model
a git branching model defines or determine when and how changed are made and committed to a specific codebase. the benefit of using a git branching model is that it helps to expendite or speed up of the process of delivering feedback to devs. It is good to remember that a **git branching model** does not come oout of the box with git hosting solutions.
these git branching models help overcome branching pattern design challenges that might eventually come up.
#### Git branching model types
- feature branching model
  this is a type of branching model that deals with devs creating a branch off the main codebase to work on a new feature, which means that they can work on the new feature without affecting the main branch itself. when the dev is done, he/she can now merge their new code into the main branch after it has been reviewed.
  it is worth noting that teams that work in this way tend to have more branches, and proiritze solo devs work. the type of branching model is also called: **task branching** or **issue branching**. Besides creating new features, this branching model is also great for fixing bugs or working on Jira tickets, because they are feature branches more shortlived and works best with fast paced codebases.

  ##### Pros and Con
  - the biggest benefit in using this branching model is that there is always one source of truth, which might be the main branch.

  ##### Con
  - the biggest con on using this branching model is that the chances for a potential **merge conflicts** might increase due to devs working isolation and technical debts might increase.

- release branching strategy
  this is when the entire codebase is branched before a new release is pushed out. the released branch should be stable with little or no changes originating from the release branch itself. this strategy is required for teams that have to handle multiple releases or patches over time. An example would be teams handling multiple versions of a product like **android or apple apps**.

  ##### Pros
  - the biggest benefit in using this strategy is that is gives you a lot of control over releases, in terms of prioritising and pushing releases out on time.
 
  ##### Con
  - the biggest con when using this strategy is that the number of releases can easily get out of hand and the potential for regression and code instability might increase.
 
- trunk-based branching strategy
 this type of branching strategy deals with commiting code directly into the mainline. which is also called the **trunk**. teams using this strategy usually commit their changes several times a day, resulting in the production of smaller updates.

  ##### Pros
  - the biggest benefit in this is **continuous integration and deloyment** (which is good because frequently committing changes to a central codebase encourages the team to align to best practices, and keeps the code repositories up to date.
  - faster feedback cirlces because code is committed multiple times of day, which leads to more speedier feedback.
  - enchanced collaboration is often the result of this strategy because members are required to work more closely, therefore strengthening communication.
  - fewer merge conflicts occur because a team member regularly commits his/her changes, which leads to spending less time on solving merge conflicts.
  - fewer branches to maintain, which leads developement to stay organized and manageable.
  - 
   ##### Con
  - the biggest drawback using this strategy is that new code is visible to everyone, which might lead to interference or the duplication of work.
  - branch destablizations might happen since everyone is working on the same branch, which can lead to increased dev frustration.
  - challenging to scale because you have multiple devs commiting at the same time or commit large changes.

###  Conclusion
It's not necessarily compulsory to use only of these branching strategies, but you can rather combine them according to your project's need. For example, your team could use a trunk-based strategy when working on small hot fixes or features, and use the feature or release branching strategy when working on big features.
