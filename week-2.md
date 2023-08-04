# Using Bash

### Configuring the Shell Environment

A configuration file is the basis for automation and customization of a Shell Environment. It means you don't have to set averything up
every time you are working in a new machine, it allows a range of machines in a cluster level to have the same configuration.  
This configuration has to be inside a invisible file: /.bashrc
  - alias -> shortcuts
  - source -> environment
    - python env
  - functions -> custom code

### Configuring .bashrc

.bashrc file is executed everytime a new shell is started, it contains commands and configurations used in that environment.  

When you open a new terminal or start a new shell session, Bash reads and automatically executes the content of the .bashrc 
file to configure the environment based on the definitions and customizations contained in it. This includes environment variables, 
aliases, functions, and other Bash-specific settings.

The purpose of the .bashrc file is to allow you to personalize the behavior of your shell according to your preferences by adding 
shortcuts, useful variable definitions, or other specific settings that you want to apply in all interactive Bash sessions.
