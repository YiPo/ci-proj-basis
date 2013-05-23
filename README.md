
# ci-proj-basis

A project template providing a better way to develop and deploy a website based on CodeIgniter framework.

## Features

* Use [CodeIgniter](http://ellislab.com/codeigniter) as a web framework.
	- Omit `index.php` in URL no matter where you place your website  
	(at document root, its subdirectory, or on a virtual host).
* Use [Git](http://git-scm.com/) as a version control system.
	- With pre-configured `.gitignore`.
	- Update CodeIgniter by updating the [system submodule](https://github.com/YiPo/ci-proj-system).
* Develop and test at local and then deploy to the live website.
	- The project is deploying-independent and easy to set up.
	- Deploy the website by `git push`.
* User-friendly configuration panel.
* The private zone.
* Compatible with Linux and Windows.

## Usage

### Create a New Repo

1. Download the [latest project template](https://github.com/YiPo/ci-proj-basis/archive/master.zip), and unzip it.

2. Rename the folder `ci-proj-basis-master` as your own project name.

3. Change directory to the folder, and execute the following commands:

	```
	git init
	git submodule add git://github.com/YiPo/ci-proj-system.git private/system
	git add .
	git commit -m "Initial commit"
	```

4. Push this local repo to your remote repo.

	```
	git remote add origin <your-remote-repo>
	git push -u origin master
	```

### Deployment

#### The Concept

Read this article: [Using Git for Deployment](http://danbarber.me/using-git-for-deployment/).

#### Remote and Website are on the Same Host

Create the file `post-receive` in the `hooks` folder of the `remote` repo as follow:

```sh
#!/bin/sh
cd <path-to-webstie>
unset GIT_DIR
git pull
git submodule update --recursive
```

and make sure the file is executable.

```
chmod +x post-receive
```

#### Remote is on GitHub

Set the *webhook URL* to the page `ci-proj-admin/deploy.php` of your website, see [Post-Receive Hooks](https://help.github.com/articles/post-receive-hooks) for more information. You should set a password from the admin panel to restrict the accessing to the page. So your *webhook URL* may looks like this:

```
https://user:password@hostname.com/path/to/website/ci-proj-admin/deploy.php
```

### Clone a Repo

Run this command:

```
git clone --recursive <your-remote-repo>
```

or execute the following command after cloning.

```
git submodule update --init --recursive
```

### Configuration

Link to the page `ci-proj-admin/` of your website.

### Private Zone

The `private` folder and anything in it are unreachable from the web.
