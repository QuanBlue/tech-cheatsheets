# Workflow files Example

After `Push`, `Pull Request`, or `Workflow Dispatch` event trigger workflow, we can see the workflow in `Actions` tab.

<div align="center">

![Action board](./assets/action_board.png)
<i>Figure 1: Action board</i>

</div>

We can see, 2 workflows are `triggered`. and `complete`. Let's inspect the `Hello World` workflow.

<div align="center">

![Hello World workflow (1)](./assets/hello_workflow_1.png)
<i>Figure 2: Hello world workflow</i>

</div>

There are 2 jobs in this Workflow: `Get user name` and `Say hello`. Let's inspect the `Get user name` job.

<div align="center">

![Hello World workflow (2)](./assets/hello_workflow_2.png)

<i>Figure 3: Hello world workflow - Get user name job</i>

</div>

All Task is `completed`, and we can see the `output` of each task.

Let's inspect the `Get user name` job.

<div align="center">

![Hello World workflow (3)](./assets/hello_workflow_3.png)

<i>Figure 4: Hello world workflow - Say hello job</i>

</div>
All Task is `completed`, and we can see the `output` of each task.

Turn out to `Secret` workflow, we can see the `Secret` workflow is `triggered` and `complete` too.

<div align="center">

![Secret workflow (1)](./assets/secret_workflow_1.png)

<i>Figure 5: Secret workflow</i>

</div>

There are a job in this Workflow: `Fetch secrets`. Let's inspect the `Fetch secrets` job.

![Secret workflow (2)](./assets/secret_workflow_2.png)

All Task is `completed`, and we can see the `output` of each task.

In 2 task `Load secrets into environment variables` and `Read secret directly`, we can see the `Secrets` value is `masked` by `***`. This is Github's security feature to prevent `Secrets` value leak to `log`.

To set the `Secrets` value, we can go to `Settings > Secrets and variables > Actions` tab. Figure bellow show the secret key I have set.

<div align="center">

![repo secret](./assets/repo_secret.png)

<i>Figure 6: Repo secret</i>

</div>
