Example scripts to run multiple commands on a router and save to an individual file per router

Example 1 - 

playbook: cmd_report1.yml
Jinja Template: report1.j2
Output directory: output1

A separate task for each command. Command output is register to a variable and the variable is he jinja template report1.j2.

The report is generated using jinja2 

To add additional commands:

1. Add new command task in playbook and register to a unique variable
2. Update jinja2 template with new variable to capture output



Example 2:

playbook: cmd_report2.yml
Jinja Template: report2.j2
Output directory: output2

A bit more elegant. All commands are saved as yaml files in the cmd_dir directory. These are then called in the cmd_report2.yml playbook via an include and using "with_fileglob" which allows us to use a wildcard to select all yaml files in the cmd_dir directory. all tasks in the cmd_dir is run against each host.

The jinja template then loops through the output to generate the report, as all registered variables become a variable of
hostvars[inventory_hostname]

To add additional commands

1. Add new yml file with addtional command in teh cmd_dir directory, dont forget to update the registered variable. No need to update the jinja template


