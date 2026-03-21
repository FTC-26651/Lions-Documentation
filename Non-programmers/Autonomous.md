# Autonomous

So, you don't know how to code but want to work on an auto? Well, do I have news for you. It is really not that hard.

## Getting Started
First off, you'll want to plot the course of the robot in [Pedro's Visualizer](https://visualizer.pedropathing.com/). Now, through some infrastrcuter that isn't built out quite yet, you'll turn that into a file with the .yaml extension, otherwise known as a yaml. Take that yaml and put it into the assets folder of the team code folder (`FtcRobotController\TeamCode\src\main\assets`).

Secondly, you'll want to create or edit a yaml file. That yaml file will also go into assets. Editing a yaml file is simple. Basically, you'll want to have a line called `commands:`. Then, after that, each action you want to take will be denoted by `- name:`. After that, put whatever system you want to use, along with any parameters on the next lines. This is clearer when you have a yaml to look at, so here is an example yaml that turns on the intake, follows a path called path 1, and turns off the intake.
```yaml
commands:
  - name: intake
    action: on
  - name: path 1
    hold end: false
    max power: 1
  - name: intake
    action: off
```

## Commands
There are a few commands that will not change and do some things. The most noteable one is called `wait`. This takes in a `duration` parameter in miliseconds. The following code waits for 5 seconds:
```yaml
  - name: wait
    duration: 5000
```