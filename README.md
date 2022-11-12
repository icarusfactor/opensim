Welcome to OpenSimulator (OpenSim for short)!

# Forked EXPERIMENTAL User Remove Overview 

This modification currently is for adding a Console command for removing users from the database. 
No checks are currently employed for my modification, but will need to be. I have been made aware 
that when Opensim is in the HG setup configuration this will cause huge database garbage build up
and create many origin connection issues when owner UUID becomes missing. The reason I made this 
was when setting up the Opensim Wordpress account sync. This can be eaily abused if Wordpress is
 not setup with these precautions and just to manually remove users so they dont show back up in 
Wordpress if the user rmeoves their account. 

CONSOLE COMMAND:
```
remove user [<user uuid>]
ex: remove user f9068f07-ed88-454d-be04-46e5be39b625
```

This UUID can be found in the Opensim datbaase table under UserAccounts with the label PrincipalID.
This is a test user to insert SQL query command to use to create as a test user to delete. 
```
INSERT INTO UserAccounts VALUES ("f9068f07-ed88-454d-be04-46e5be39b625","00000000-0000-0000-0000-00000000000","Jim", "Bob","factor@userspace.org", "HomeURI=http%3a%2f%2fopensim.spotcheckit.org%3a9000%2f",1665681721,0,0,"",1);
delete from UserAccounts where PrincipalID = f9068f07-ed88-454d-be04-46e5be39b625;
```
SQL query that is used in the remove command.
```
delete from UserAccounts where PrincipalID =  'f9068f07-ed88-454d-be04-46e5be39b625';
```

MY BUILD PROCESS:
```
make clean
./runprebuild48.sh
msbuild /p:Configuration=Release
```

REFRENCE OF PROBLEM TO OVERCOME:
https://blog.zetamex.com/posts/2021/11/drowning-in-garbage/

OPENSIM WIKI:(Excerpt about user removal)
This is probably not currently possible. Or rather, nobody has done it and reported back whether 
everything still works or whether there are lots of issues. The normal way to 'delete' a user is  
to set their UserLevel to -1. This will prevent them from logging in.


If anyone has ideas or patches please add them to the issues section and I will follow up. 


# Overview

OpenSim is a BSD Licensed Open Source project to develop a functioning
virtual worlds server platform capable of supporting multiple clients
and servers in a heterogeneous grid structure. OpenSim is written in
C#, and can run under Mono or the Microsoft .NET runtimes.

This is considered an alpha release.  Some stuff works, a lot doesn't.
If it breaks, you get to keep *both* pieces.

# Compiling OpenSim

Please see BUILDING.md if you downloaded a source distribution and 
need to build OpenSim before running it.

# Running OpenSim on Windows

You will need .NET 4.0 for versions up to 0.9.0.1 and .NET 4.6 for others.

We recommend that you run OpenSim from a command prompt on Windows in order
to capture any errors.

To run OpenSim from a command prompt

 * cd to the bin/ directory where you unpacked OpenSim
 * review and change configuration files (.ini) for your needs. see the "Configuring OpenSim" section
 * run OpenSim.exe or opensim32.exe for small regions


# Running OpenSim on Linux

You will need Mono >= 2.10.8.1 up to version 0.9.0.1 and mono > 5.0 on others.  On some Linux distributions you
may need to install additional packages.  See http://opensimulator.org/wiki/Dependencies
for more information.

To run OpenSim, from the unpacked distribution type:

 * cd bin
 * review and change configuration files (.ini) for your needs. see the "Configuring OpenSim" section
 * run ./opensim.sh


# Configuring OpenSim

When OpenSim starts for the first time, you will be prompted with a
series of questions that look something like:

	[09-17 03:54:40] DEFAULT REGION CONFIG: Simulator Name [OpenSim Test]:

For all the options except simulator name, you can safely hit enter to accept
the default if you want to connect using a client on the same machine or over
your local network.

You will then be asked "Do you wish to join an existing estate?".  If you're
starting OpenSim for the first time then answer no (which is the default) and
provide an estate name.

Shortly afterwards, you will then be asked to enter an estate owner first name,
last name, password and e-mail (which can be left blank).  Do not forget these
details, since initially only this account will be able to manage your region
in-world.  You can also use these details to perform your first login.

Once you are presented with a prompt that looks like:

	Region (My region name) #

You have successfully started OpenSim.

If you want to create another user account to login rather than the estate
account, then type "create user" on the OpenSim console and follow the prompts.

Helpful resources:
 * http://opensimulator.org/wiki/Configuration
 * http://opensimulator.org/wiki/Configuring_Regions

# Connecting to your OpenSim

By default your sim will be available for login on port 9000.  You can login by
adding -loginuri http://127.0.0.1:9000 to the command that starts Second Life
(e.g. in the Target: box of the client icon properties on Windows).  You can
also login using the network IP address of the machine running OpenSim (e.g.
http://192.168.1.2:9000)

To login, use the avatar details that you gave for your estate ownership or the
one you set up using the "create user" command.

# Bug reports

In the very likely event of bugs biting you (err, your OpenSim) we
encourage you to see whether the problem has already been reported on
the [OpenSim mantis system](http://opensimulator.org/mantis/main_page.php).

If your bug has already been reported, you might want to add to the
bug description and supply additional information.

If your bug has not been reported yet, file a bug report ("opening a
mantis"). Useful information to include:
 * description of what went wrong
 * stack trace
 * OpenSim.log (attach as file)
 * OpenSim.ini (attach as file)
 * if running under mono: run OpenSim.exe with the "--debug" flag:

       mono --debug OpenSim.exe

# More Information on OpenSim

More extensive information on building, running, and configuring
OpenSim, as well as how to report bugs, and participate in the OpenSim
project can always be found at http://opensimulator.org.

Thanks for trying OpenSim, we hope it is a pleasant experience.

