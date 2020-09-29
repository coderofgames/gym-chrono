**Status:** Under Active Development (New Environments and features will be added)
> :warning: **These environment are compatible with the develop version of ChronoAPI**: Checkout develop branch if you build from [sources](https://github.com/projectchrono/chrono) or use develop label if you install with [Anaconda](https://anaconda.org/projectchrono/pychrono)
# gym-chrono

Gym Chrono is a set of continuous state and action spaces DRL environmentbased on the open-source physics engine [Project Chrono](https://projectchrono.org/). 
In order to run these environment you need to install [PyChrono](https://projectchrono.org/pychrono/). 
Being part of Project Chrono, PyChrono is **free and open-source**. Moreover, it provides an [Anaconda installer](https://anaconda.org/projectchrono/pychrono).
Currently, these tasks are supported:

**chrono_pendulum-v0** 


![](http://projectchrono.org/assets/manual/Tutorial_tensorflow_pendulum.jpg)

Reverse pendulum, the goal is to balance a pole on a cart.  1 action (force along the z axis) and 4 observations (position and speed of cart and pole).

**chrono_ant-v0** 


![](http://projectchrono.org/assets/manual/Tutorial_tensorflow_ant.jpg)

A 4-legged walker, the goal is learning to walk straight as fast as possible. 8 actions (motor torques) and 30 observations (GOG height, COG speed, COG orientation in Euler Angles, COG rotational speed, joints rotation, joints speed, feet contact).

**chrono_hexapod-v0** 


![](https://github.com/projectchrono/chrono-web-assets/blob/master/Images/Hexapod.jpg)

A 6-legged walker, the goal is learning to walk straight as fast as possible. Heach legs counts 3 actuated joints.
18 actions (motor torques) and 53 observations (GOG height, COG speed, COG orientation in Euler Angles, COG rotational speed, joints rotation, joints speed, feet contact).

This is a model of a real hexapod robot, the PhantomX Hexapod Mark II. Motors dara are available [here](https://trossenrobotics.com/dynamixel-ax-12-robot-actuator.aspx). Credit to [Hendricks](https://grabcad.com/hendricks-1) for the CAD drawings.

**ChronoRacer3Reach-v0** 


![](https://github.com/projectchrono/chrono-web-assets/blob/master/Images/Comau.jpg)

A 6-DOF robotic arm (Comau Racer-3), the goal is minimizing the distance between the center of the gripper and the center of the red target box. CAD files and part of the techical data are freely available from the Comau website [here](https://www.comau.com/IT/le-nostre-competenze/robotics/robot-team/racer-3-063) .
6 actions (motor torques) and 18 observations (joints rotation, joints speed, end-effector position, target position).

# Installation
Please follow each step of these instructions. They will help you make an Conda environment that has all the packages you will need to work with gym-chrono.

### Requirements
1. conda
- You can check if you already have this by running `conda --version`.
- To install, see the instructions [here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/).
- You can use Anaconda or Miniconda; either will work.

### 1. Clone the gym-chrono repository.
```
git clone https://github.com/projectchrono/gym-chrono.git
```

### 2. Conda Environment Setup
2.1 Move into the gym-chrono repository.
```
cd gym-chrono
```

2.2 Checkout the branch with the .yml Conda environment file.
```
git checkout tutorial_solution
```

2.3.A. Use the .yml to create a new Conda environment with the necessary packages.
```
conda env create -f conda_env_gym_chrono_tutorial.yml
```
2.3.B. Alternatively, follow these instructions:
```
conda create -n conda_env_magic_tutorial python=3.7
conda install -c anaconda tensorflow-gpu=1.14 --yes
pip install gym
conda install -c projectchrono/label/develop pychrono --yes
```
2.4. Confirm the new environment exists on your system. It should be called "gym_chrono_tutorial".
```
conda env list
```
2.5. Activate the new environment.
```
conda activate gym_chrono_tutorial
```
2.6 Complete gym-chrono installation.
```
pip install -e .
```

### 3. Install the [OpenAI Baselines repository](https://github.com/openai/baselines) and modules
3.1 Clone the repository. Note that this should be at the same directory level as where the gym-chrono repository is.
- If you've been following along with the previous installation steps, you'll have to move out of the gym-chrono repository.
```
cd ..
```
Then clone the baselines repository.
```
git clone https://github.com/openai/baselines.git
```
Your file structure should now look like this.
```
.
├── baselines
└── gym-chrono
```
3.2 Complete baselines installation.
```
pip install -e ./baselines/
```

### 4. Example
Great! Now we can run an example. The line below will train the ant environment using the PPOalgorithm in [OpenAI Baselines](https://github.com/openai/baselines).
```
python -m baselines.run --alg=ppo2 --env=gym_chrono.envs:chrono_ant-v0 --network=mlp --num_timesteps=2e7 --ent_coef=0.1 --num_hidden=32 --num_layers=3 --value_network=copy
```

Sample output of first step (your numbers might be slightly different):

<img src="https://github.com/projectchrono/chrono-web-assets/blob/master/Images/ant_example_output.png" width=200>

### Other
- To get out of the Conda environment,
```
conda deactivate
```
- To re-activate the environment,
```
conda activate gym_chrono_tutorial
```
- If you would like to completely remove this Conda environment at a later date, use the following. Note that you must deactivate the environment first.
```
conda remove --name gym_chrono_tutorial --all
```
