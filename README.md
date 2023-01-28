# Welcome to the Microsoft Challenge @ MIT iQuHACK 2023!

## Challenge overview

In this challenge, you will explore optimizing quantum circuits, and more specficially - optimizing quantum oracles.
In each task, you'll be given a quantum oracle that implements a certain classical function (the classical function definition is not included in the task).
You'll need to rewrite the code so that it maintains its correctness, but requires as few resources as possible. 

## Working on the challenge

* The challenge contains 9 independent tasks. Your team can work on each task independently; tasks are submitted and scored separately.
* You can work on the challenge using a local Quantum Development Kit setup, Azure Quantum hosted notebooks, or qBraid platform. 
* You'll need to [create an Azure account and an Azure Quantum workspace](https://aka.ms/iQuHack2023/AQJobSubmit) to evaluate the resources used by your solution, regardless of the platform you're using.
* To work on each task, use the Jupyter notebooks iQuHack-challenge-2023-taskX.ipynb. Each notebook contains the step-by-step instructions for working on the task, including the code that helps you evaluate your solution.
* **You will submit the tasks for challenge using qBraid platform.**
  Each task submission is evaluated automatically in two steps. 
  1. First, the task correctness is checked by verifying that your code acts the same as the original oracle implementation.  If your solution doesn't compile, throws a runtime error, or acts differently from the original oracle implementation, this submission will be ignored.
  2. Second, if the task is logically correct, its resource consumption is evaluated. For this, we submit a resource estimation job for your code, and calculate your score as **(logical algorithmic qubits) * (algorithmic depth)** (see [resource estimation documentation](https://learn.microsoft.com/en-us/azure/quantum/learn-how-the-resource-estimator-works#algorithmic-logical-estimation), [introductory workshop](https://www.twitch.tv/videos/1718264700) or resource estimation samples for the meaning of these parameters).
  3. Your goal is to minimize your score for each task. Your aggregate score in the scoreboard is a sum of ratios (your score for the task) / (the score of the initial oracle implementation for the task) for all tasks.


### Tips and tricks for optimizing your quantum programs

**The score is defined as a product: (logical algorithmic qubits) * (algorithmic depth)**

* The number of logical qubits after mapping scales proportional to the number of qubits in the circuit. Therefore, reducing the qubits in the circuit always helps, unless it leads to an increase in operations.
* The number of logical cycles depend on the number of Toffoli gates (translated to CCZ), T gates, single-qubit measurements (which you will not be using in this challenge), and rotation gates. Clifford operations do not increase logical cycles.
* Rotation gates are the most expensive ones and should be avoided when possible! (For this challenge, you should be able to avoid them completely, using only reversible computation)
* Multiple-controlled X gates (multiple-controlled Toffoli gates) are decomposed by the resource estimator. The number of cycles is 3 * (n - 1), where n >= 1 is the number of control qubits.
* The concrete formulas to determine the logical qubits and logical cycles (after mapping) from the input program is provided in the paper https://arxiv.org/pdf/2211.07629.pdf 
  * Number of logical qubits in (D1, page 29)
  * Number of logical cycles in (D3, page 30)


## Working on qBraid and submitting the tasks
[<img src="https://qbraid-static.s3.amazonaws.com/logos/Launch_on_qBraid_white.png" width="150">](https://account.qbraid.com?gitHubUrl=https://github.com/iQuHACK/2023_microsoft.git)
1. If you're working on qBraid, first fork this repository and click the above `Launch on qBraid` button. It will take you to your qBraid Lab with the repository cloned.
2. Once cloned, open terminal (first icon in the **Other** column in Launcher) and `cd` into this repo. Set the repo's remote origin using the git clone url you copied in Step 1, and then create a new branch for your team:
```bash
cd  <microsoft_git_repo_name>
git remote set-url origin <url>
git branch <team_name>
git checkout <team_name>
```
3. Use the environment manager (**ENVS** tab in the right sidebar) to activate the "Microsoft Q#".  click **Activate** to [add a new ipykernel](https://qbraid-qbraid.readthedocs-hosted.com/en/latest/lab/kernels.html#add-remove-kernels) for "Microsoft Q#".

<img width="287" alt="image" src="https://user-images.githubusercontent.com/32727721/214965872-f69be46b-64b3-47c0-883d-1ee87374f68b.png">


4. From the **FILES** tab in the left sidebar, double-click on the `2023_Microsoft_Challenge` directory.

5. You are now ready to begin hacking! Work with your team to complete the Microsoft Q# Challenge.


### qBraid Auto Grader Submission Process To Leaderboard:

**PLEASE MAKE SURE TO DO THE FOLLOWING BEFORE YOU SUBMIT**

- Your team name, task #, and a point person's slack name (just in case we need to reach out).
Once you have completed any of the tasks and have added the team name, task # and a point person's slack name, if you are confused). Please got to File (**File** on the top left of the topbar) and click on the `Share notebook` button.
<img width="319" alt="スクリーンショット 2023-01-26 午後4 42 50" src="https://user-images.githubusercontent.com/32727721/214967319-3d2f64ec-19f8-4a06-bf20-0690f8f0e29e.png">

- Enter `rickyyoung@qbraid.com` and share the file. If it shares successfully, the email should dissapear. Ricky will periodically run the autograder and the leaderboard will be updated accordingly.

- Then submit the remote project submission form that will show up on the iQuHACK website during the last 8 hours of hacking. The form will ask for a link to your repository and your team members (all of whom have to be remote iQuHACK participants to maintain elligibility).

## Prizes

Up to (3) teams with the highest team scores will be chosen as the winners of the Hackathon.
Each member of the winning teams will get a Surface 2 headset.

## Resources

* [Introduction to Azure Quantum workshop at MIT iQuHack](https://www.twitch.tv/videos/1718264700), Wednesday, January 25, 2023
* [The Quantum Katas](https://github.com/Microsoft/QuantumKatas/) - a collection of tutorials and practice problems (chapters "Quantum Oracles and Simple Oracle Algorithms" and "Grover's search algorithm" are a good place to practice your work with marking oracles)
* [Getting started with the resources estimator service](https://learn.microsoft.com/en-us/azure/quantum/quickstart-microsoft-resources-estimator)
* [A deep dive in resource estimation](https://arxiv.org/pdf/2211.07629.pdf)
* [Azure Quantum and Microsoft Quantum Development Kit documentation](https://learn.microsoft.com/azure/quantum/)
