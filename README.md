# Service Wrapper
The `service_wrapper` payload is a special payload. This is a .NET 3.5/4.0 service executable that acts as a "wrapper" around another agent. As such, this payload type has no commands and no supported C2 profiles - it simply acts as a way to turn arbitrary other agents into properly formatted Windows Service Executables.

This payload type is for Mythic 2.2.7 and reports as version "8". It is not compatible with Mythic version 2.1.

## How to install an agent in this format within Mythic

When it's time for you to test out your install or for another user to install your agent, it's pretty simple. Within Mythic you can run the `mythic-cli` binary to install this in one of three ways:

* `sudo ./mythic-cli install github https://github.com/user/repo` to install the main branch
* `sudo ./mythic-cli install github https://github.com/user/repo branchname` to install a specific branch of that repo
* `sudo ./mythic-cli install folder /path/to/local/folder/cloned/from/github` to install from an already cloned down version of an agent repo

Now, you might be wondering _when_ should you or a user do this to properly add your agent to their Mythic instance. There's no wrong answer here, just depends on your preference. The three options are:

* Mythic is already up and going, then you can run the install script and just direct that agent's containers to start (i.e. `sudo ./mythic-cli payload start agentName` and if that agent has its own special C2 containers, you'll need to start them too via `sudo ./mythic-cli c2 start c2profileName`).
* Mythic is already up and going, but you want to minimize your steps, you can just install the agent and run `sudo ./mythic-cli mythic start`. That script will first _stop_ all of your containers, then start everything back up again. This will also bring in the new agent you just installed.
* Mythic isn't running, you can install the script and just run `sudo ./mythic-cli mythic start`. 

## Icon

https://www.flaticon.com/free-icon/sweet_3050124

<a href="https://www.flaticon.com/free-icons/sugar" title="sugar icons">Sugar icons created by Freepik - Flaticon</a>
