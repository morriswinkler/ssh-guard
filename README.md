# ssh-guard
--
Command ssh-guard is a simple tool to manage allowed ssh commands via the
authorized_keys command parameter.

### Install

    go get github.com/morriswinkler/ssh-guard


### Setup

Upload a public ssh rsa key to the user folder on your ssh server, for my user
id would be at:

    /home/morriswinkler/.ssh/authorized_keys

Prepend the key with the command parameter:

    cat /home/morriswinkler/.ssh/authorized_keys
    commadn="/home/morriswinkler/go/bin/ssh-guard" ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDyGB4+u1qRBNOpDGtQm1LgJXJMmRo+Dvu4WKbpwq29aSM+1KulQw+sJ9vhpKXZt5bqCCkv/2W+ScqSBP87AaFqT8tQ45f4tq6IYibYLjWT492qL948B7Yd2EEvVmP1K81uPvLLzgiuZ3Ci/1pa7kBEmxqI7itrD7g1A9BRixq74X3S/KvhEti/Nm8BGQBrg+8h05qyHG7qtQtwajbQDZsxAEN3OseZpI2n0WFBcJ84ic5lK8f01CBtRLPvwcu8/lpn7bW5MzC0ShyBT1OMBaUwzwfAfn9Tw9aoziAzmGFbW5OkuBObQKG6pSo2Th2C40fhTO1WoefHv2FT4BxhgpVv morriswinkler@ssh_server

Some options to make it a bit more secure:

    cat /home/morriswinkler/.ssh/authorized_keys
    from="8.8.8.8",no-port-forwarding,no-X11-forwarding,no-agent-forwarding,no-pty,commadn="/home/morriswinkler/go/bin/ssh-guard" ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDyGB4+u1qRBNOpDGtQm1LgJXJMmRo+Dvu4WKbpwq29aSM+1KulQw+sJ9vhpKXZt5bqCCkv/2W+ScqSBP87AaFqT8tQ45f4tq6IYibYLjWT492qL948B7Yd2EEvVmP1K81uPvLLzgiuZ3Ci/1pa7kBEmxqI7itrD7g1A9BRixq74X3S/KvhEti/Nm8BGQBrg+8h05qyHG7qtQtwajbQDZsxAEN3OseZpI2n0WFBcJ84ic5lK8f01CBtRLPvwcu8/lpn7bW5MzC0ShyBT1OMBaUwzwfAfn9Tw9aoziAzmGFbW5OkuBObQKG6pSo2Th2C40fhTO1WoefHv2FT4BxhgpVv morriswinkler@ssh_server

Thats it you are ready to roll.


### CommandManagement

By default no command is allowed, you can add commands by running:

    ssh-guard -add "ls /"

To list them use:

    ssh-guard -list

And finaly to remove them use:

    ssh-guard -del 1

Commands are stored as a colon separated list in ~/.config/ssh-guard/config.ini:

    allowed_commands = ls /: ps aux:ls

The log file contains ignored and allowed commands and invoations from the sshd,
you can use it to find commands to add if needed. You can change the location
inside the config.

    logfile = ~/ssh-gaurd.log
