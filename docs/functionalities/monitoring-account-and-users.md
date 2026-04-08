This section describes many secondary functionalities for project management. 

## Account page

The account page allows user to change their password. If you have forgotten your password, please reach out to the instance manager.

## Users page

This page allows users to manage collaboration rights across people and projects.

![](../img/functionalities/users.png)

Three roles are defined with different rights: 

- <span class="highlight">root</span>: Only one root account. This user can manage the rights of anyone and has access to **ALL** projects as a manager. Root has also access to the [Monitor page](#monitor-page).
- <span class="highlight">manager</span>: Default role when creating a project. Managers have access to the data, can annotate, train models, compute features, and delete anything. 
- <span class="highlight">collaborator</span>: Collaborators have the same rights as mangers but cannot delete anything.
- <span class="highlight">annotator</span>: Annotators only have access to the [Codebook page](./codebook.md), [Explore page](./explore.md) and the [Annotate page](./annotate.md).

Each role is project dependant and can be managed by managers of a project. After selecting the appropriate project, they can type the name of a user and grant them the appropriate rights.

## Monitor page

This page is only visible by the root user. It contains multiple panels described below

### Active project tab

![](../img/functionalities/monitor-active-projects.png)

This page lists all projects currently in use and associated tasks (train classifiers for instance) currently running. From this tab, the root user can kill any task.

<span class="action red-danger">Restart memory and queue</span> will restart the backend. All current users will be impacted and active tasks killed. 

### Statistics tab

![](../img/functionalities/monitor-statistics.png)

This page lists all completed tasks and the computing time to assess the installation efficiency. Each task is associated with a user and a project.

### Messages tab

![](../img/functionalities/monitor-messages.png)

This page allows the root user to leave messages on the frontpage of the app in order to warn users of recent bugs, upcomming memory wipe or maintenance. 

### Logs tab

This page lists all actions performed (annotation, train models, inference ...) with a time stamp, and the assiociated user and project.

### Resources tab

This page lists the resources detected and usable by the app (GPU, CPU, Memory and disk).

### Users tab

This page lists the existing accounts with all the projects they are involved in as well as their role.
