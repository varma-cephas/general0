### Git Branching Model
a git branching model defines or determine when and how changed are made and committed to a specific codebase. the benefit of using a git branching model is that it helps to expendite or speed up of the process of delivering feedback to devs. It is good to remember that a **git branching model** does not come oout of the box with git hosting solutions.
these git branching models help overcome branching pattern design challenges that might eventually come up.
#### Git branching model types
- feature branching model
  this is a type of branching model that deals with devs creating a branch off the main codebase to work on a new feature, which means that they can work on the new feature without affecting the main branch itself. when the dev is done, he/she can now merge their new code into the main branch after it has been reviewed.
  it is worth noting that teams that work in this way tend to have more branches, and proiritze solo devs work. the type of branching model is also called: **task branching** or **issue branching**. Besides creating new features, this branching model is also great for fixing bugs or working on Jira tickets, because they are feature branches more shortlived and works best with fast paced codebases.
  the biggest benefit in using this branching model is that there is always one source of truth, which might be the main branch. the biggest con on using this branching model is that the chances for a potential **merge conflicts** might increase due to devs working isolation and technical debts might increase.

- 
