# AnsiblePress
A minimal WordPress (LEMP) development environment using: Vagrant, Virtualbox, Ansible, Ubuntu, Nginx, MySQL, and PhP. This is meant to be a quick and easy boilerplate for continued development.

##Quick Setup
1. Install Vagrant and Virtual Box
2. Create a project directory `example.com` then cd into it `cd example.com` 
3. Run `git clone git@github.com:jeanpierreb/AnsiblePress.git`
4. Run `git clone git@github.com:WordPress/WordPress.git`
5. From your AnsiblePress directory run `vagrant up`

Directory Structure
<pre>
├── example.com
│   ├── AnsiblePress
│   ├── WordPress
</pre>

All that's left is to go to wp.dev in your browser and follow WordPress's famous 5-minute installer and start working.

##Custom Url
In OSX add this to the end of your `/ect/hosts` file
```
192.168.50.50    wp.dev
```

**[From Vagrant's Docs](http://docs.vagrantup.com/v2/networking/private_network.html)**

>While you can choose any IP you'd like, you should use an IP from the reserved private address space. These IPs are guaranteed to never be publicly routable, and most routers actually block traffic from going to them from the outside world.

##Aliases
I added some helper files extracted from my dotfiles repo. You can check them out here if you want more details.

Shortcuts included:
```bash
alias ..="cd .."
alias ...="cd ../.."
alias ....="cd ../../.."
alias .....="cd ../../../.."
alias ~="cd ~" # `cd` is probably faster to type though
alias web="cd /etc/nginx/sites-available"
alias wpdir="cd /var/www/wordpress/"

# List all files colorized in long format
alias l="ls -lF ${colorflag}"

# List all files colorized in long format, including dot files
alias la="ls -laF ${colorflag}"

# List only directories
alias lsd="ls -lF ${colorflag} | grep --color=never '^d'"

alias restart="sudo service nginx restart; sudo service php5-fpm restart"
alias status="service nginx status; service php5-fpm status; service mysql status"
```

##Variables
The only file you should have to touch is the `group_vars/all` It's pretty self explanatory, all you need to do is add your names, passwords and database credentials and ansible will handle the rest.

```bash
site: {
  name: wp.dev,
  ip: "192.168.50.50", #Be sure to change this in your VagrantFile as well
  www_root: /var/www/wordpress #there should be no reason to change this but you can.
}

database: {
  name: wordpress, #Database name
  user: wordpress, #Database user given all privs in the database
  password: password #Database user's password
}
```

##Contributions
Pull requests are always welcome OR If you see a bug or error just open a new [issue](https://github.com/jeanpierreb/AnsiblePress/issues)
