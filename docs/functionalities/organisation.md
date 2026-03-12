# Documentation

<!-- TODO: Include layout description -->

This documentation details the different logics and functionalities of Active Tigger. It is a work in progress. It will be updated as the project evolves. 

*If you see features that need more explanations, please open an issue.*


## Accounts and rights

ActiveTigger is based on a dual system of rights : type of accounts and rights on projects.

A user account can have one of the following status :

- **root**: can do everything (especially access all projects and the /monitor page)
- **manager**: can create new projects and manage them (adding users on those projects)
- **annotator**: can only annotate on projects with a simplified frontend

Users have specific rights on projects :

- **manager**: can manage the project, add users, launch processes and access data.
- **contributor**: can create elements in a project (scheme, annotation, model) but never delete things
- **annotator**: can only annotate on the project without changing the project settings (schemes, labels, models, etc.).

Comments :

- There is no management at the scheme level


## Queue and processes

Users can compute models. Each run is called a *process*. By default, only one process is allowed at the same time by user. There are two types of processes in Active Tigger:

- **CPU processes**: they are used to prepare data, train quick models, etc.
- **GPU processes**: these processes are using GPU if available in the server. By default, the configuration of the server only accept one GPU process at once.

Comments :

- Some processes are costly to run and can take time
- If processes are launched and no worker is avaiable, processes are put in a queue and wait for available workers.
- When launching a process, you can stop it with the "Stop" button or with the <span class="icon">![](../img/icons/stop.svg)</span>


<!-- TODO : Mention the auto log off behaviour -->

<!-- TODO : explain what objects are shared accross projects / users -->