# Documentation

<!-- TODO: Include layout description -->

This documentation details the different logics and functionalities of Active Tigger. It is a work in progress. It will be updated as the project evolves.

## General comments

Only one process allowed at the same time by user. There are two types of processes in Active Tigger:

- CPU processes: they are used to prepare data, train quick models, etc.
- GPU processes: these processes are run on the GPU. The server can only run a limited number of GPU processes at the same time.

In both cases, if the number of processes is too high, they will be queued.

## Accounts

A user can have the following status :

- **root**: can create and manage projects, users, and all data. Can access all projects and the /monitor page.
- **manager**: can create and manage projects where he.she has complete rights. Can add users to the projects.
- **annotator**: can only annotate on projects where he.she have been added. The frontend is simplified for this role.

User have also a relational status for a specific project:

- **manager**: can manage the project, add users, and access all data.
- **contributor**: can create elements in a project but never delete things
- **annotator**: can only annotate on the project without changing the project settings (schemes, labels, models, etc.).

For the moment, there is no management at the scheme level.


## Dynamic 

When launching a process, you can stop it with the "Stop" button or with the <a class="icon">![](../img/icons/stop.svg)</a> ...

<img class="specific-class" src="/img/functionalities/stop-button.png" />


<!-- TODO : Mention the auto log off behaviour -->