# A Test Oracle for Reinforcement Learning Software based on Lyapunov Stability Control Theory

## Abstract

Reinforcement Learning (RL) has gained significant attention in recent years. As RL software becomes more complex and infiltrates critical application domains, ensuring its quality and correctness becomes increasingly important. An indispensable aspect of software quality/correctness assurance is testing. However, testing RL software faces unique challenges compared to testing traditional software due to the difficulty in defining the outputs’ correctness. This leads to the RL test oracle problem.

Current approaches to testing RL software often rely on human oracles, i.e., convening human experts to judge the correctness of RL software outputs. This heavily depends on the availability and quality (including the experiences, subjective states, etc.) of the human experts and cannot be fully automated.

In this project, we propose a novel approach to design test oracles for RL software by leveraging the Lyapunov stability control theory. By constructing Lyapunov functions to guide RL training, we hypothesize that correctly implemented RL software shall output an agent that respects Lyapunov stability control theories. Based on this heuristic, we propose a Lyapunov stability control theory-based oracle, the LPEA oracle, for testing RL software. We conduct extensive experiments to evaluate the effectiveness of the LPEA oracle.

## Before Stards

Some of the commands only work on Linux/Mac. Please conduct the experiment in a Linux VM if you are using a windows machine.

## Getting Started

### Install Docker

To begin, ensure that you have Docker installed on your system. You can download it from the [Docker website](https://www.docker.com/get-started).

### Clone this repository

After installing Docker, clone this repository to your local machine. Access this repository in the terminal and follow these commands:

1. **Enter the project directory:**
   ```sh
   cd RL-Oracle-Lyapunov-v1
   ```
3. **Use 'make' command to build docker image:**
   ```sh
   make docker-cpu
   ```
5. **Interact with the docker container:**
   ```sh
   docker run -it stablebaselines/stable-baselines3-cpu:latest
   ```



Once inside the Docker container, you can follow the instructions under the **Usage** section.


## Usage


Before start, make sure you are in the **\RL-Oracle-Lyapunov-v1\RLTestingLyapunov** directory of the docker container before running the following commands.
```sh
cd ~/RL-Oracle-Lyapunov-v1/RLTestingLyapunov
```

Then:

1. **Inject a bug into the Stable-baselines library:**
    ```sh
    python bug_injection.py <bug_id>
    ```

    Replace `<bug_id>` with the specific bug id you want to inject.
    - `<bug_id>`: The id of the specific bug you want to inject. There are totally 44 bugs (0-43). Specially, bug_id = -1 means that there is no bug injected into the SB3 library. You can find detailed algorithms' bug document in **\RLTestingLyapunov\Bug library** file.

    Example command (bug-less):
    ```sh
    python bug_injection.py -1
    ```

2. **Run the LPEA Oracle:**
    ```sh
    python LPEA_Oracle.py <bug_id> <algorithm> <n> <m> <I> <J>
    ```

    - `<bug_id>`: The id of the specific bug you want to inject. There are totally 44 bugs (0-43). Specially, bug_id = -1 means that there is no bug injected into the SB3 library. You can find detailed algorithms' bug document in **\RLTestingLyapunov\Bug library** file.
    
    - `<algorithm>`: The algorithm to use (`a2c`, `ppo`, or `td3`). You can find detailed algorithms' bug document in **\RLTestingLyapunov\Bug library** file.
    - `<n>`: The dimension of the state vector (default is 2). See Section II-B Eq. (1) of the paper.
    - `<m>`: The dimension of qcontrol vector (default is 2). See Section II-B Eq. (1) of the paper.
    - `<I>`: The number of agents (also the environments) to train (default is 20). See Section III Step 1 of the paper.
    - `<J>`: The number of initial state samples for evaluation (default is 800). See Section III Step 3 - Conjecture 1 of the paper.
    
    In the demo, it is highly recommended to set a small I (like 1) to shorten the running time. In our experiment, we set I = 20 to get more stable results.

    Example command (bug-less):
    ```sh
    python LPEA_Oracle.py -1 ppo 2 2 1 800
    ```


## Results
This is an example of the output. You could check Section III for more details or vartheta and theta.

    vartheta=100%, theta=100%, the software is bug-less based on LPEA Oracle
    vartheta=100%, theta=75%, the software is bug-less based on LPEA Oracle
    vartheta=100%, theta=50%, the software is bug-less based on LPEA Oracle
    vartheta=90%, theta=100%, the software is bug-less based on LPEA Oracle
    vartheta=90%, theta=75%, the software is bug-less based on LPEA Oracle
    vartheta=90%, theta=50%, the software is bug-less based on LPEA Oracle
    vartheta=80%, theta=100%, the software is bug-less based on LPEA Oracle
    vartheta=80%, theta=75%, the software is bug-less based on LPEA Oracle
    vartheta=80%, theta=50%, the software is bug-less based on LPEA Oracle
    vartheta=70%, theta=100%, the software is bug-less based on LPEA Oracle
    vartheta=70%, theta=75%, the software is bug-less based on LPEA Oracle
    vartheta=70%, theta=50%, the software is bug-less based on LPEA Oracle
    vartheta=60%, theta=100%, the software is bug-less based on LPEA Oracle
    vartheta=60%, theta=75%, the software is bug-less based on LPEA Oracle
    vartheta=60%, theta=50%, the software is bug-less based on LPEA Oracle
    vartheta=50%, theta=100%, the software is bug-less based on LPEA Oracle
    vartheta=50%, theta=75%, the software is bug-less based on LPEA Oracle
    vartheta=50%, theta=50%, the software is bug-less based on LPEA Oracle
