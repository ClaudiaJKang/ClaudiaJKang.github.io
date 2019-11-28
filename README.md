
# Set github.io by using hugo-coder theme
> [한국어 github.io 구축 (hugo-coder 테마 사용)](https://github.com/ClaudiaJKang/ClaudiaJKang.github.io/blob/master/README_ko.md)

## 1. Install Hugo
1. Install go language.
	```sh
	# Based on fedora31
	$ sudo dnf install golang
	$ mkdir -p $HOME/go
	$ echo 'export GOPATH=$HOME/go' >> $HOME/.bashrc
	$ source $HOME/.bashrc
	```
	> [Fedora documentation - Installation go](https://developer.fedoraproject.org/tech/languages/go/go-installation.html)

2. Install Hugo.
	```sh
	# Based on github repo direcotry.
	$ cd  $HOME/go/pkg
	$ git clone https://github.com/gohugoio/hugo.git 
	$ cd hugo 
	$ go install --tags extended
	$ sudo su
	$ cd /usr/bin
	$ ln -s $HOME/go/bin/hugo hugo
	```
	> [Installation Hugo Official Documentation](https://gohugo.io/getting-started/installing/#fetch-from-github)

## 2. Set Hugo-coder theme
1. Fork the Github repository [hugo-coder](https://github.com/luizdepra/hugo-coder) of the Hugo theme to be used.
2. Create two new repositories. One repository name is `<Blog repository name>` and the other is `<username>.github.io`.
3. Create new hugo site.
	```bash
	$ hugo new site <Blog repository name> # <Blog repository name> described in number 2
	```
4. Add git remote.
	```sh
	$ cd <Blog repository name>
	$ git init
	$ git remote add origin https://github.com/<username>/<Blog repository name>.git
	$ git fetch origin
	```

5. Add theme git submodule.
	```sh
	$ git submodule add https://github.com/<username>/hugo-coder themes/hugo-coder
	```

6. Add public git submodule.
	```sh
	$ git submodule add https//github.com/<username>/<Blog repository name> public
	```

7. hugo build
	```sh
	# directory : <Blog repository name> 
	$ hugo
	```

8. Check css file name.
	```sh
	$ ls public/css
	<css file name>.css
	```

9. Set config.toml.
	```bash
	baseurl = "https://<github.io url>"
	title = "<Blog title>"
	theme = "hugo-coder"
	languagecode = "en"
	defaultcontentlanguage = "en"

	paginate = 20
	canonifyurls = true

	pygmentsstyle = "bw"
	pygmentscodefences = true
	pygmentscodefencesguesssyntax = true

	disqusShortname = "<shortname>"

	[params]
	    author = "<author name>"
	    info = "<author info>"
	    description = "<Blog description>"
	    keywords = "blog,developer,personal"
	    avatarurl = "<image url>"

	    favicon_32 = "/img/favicon-32x32.png"
	    favicon_16 = "/img/favicon-16x16.png"

	    hidecredits = false
	    hidecopyright = false

	    rtl = false

	    math = true
	    custom_css = ["css/<css file name>"]

	# Social links
	[[params.social]]
	    name = "Github"
	    icon = "fab fa-github fa-2x"
	    weight = 1
	    url = "https://github.com/<github id>/"

	# Menu links
	[[menu.main]]
	    name = "About"
	    weight = 1
	    url = "/about/"
	```

	> [hugo-coder exampleSite config.toml](https://github.com/luizdepra/hugo-coder/blob/master/exampleSite/config.toml) 
	
	> [hugo-coder config.toml configuration documentation](https://github.com/luizdepra/hugo-coder/wiki/Configurations)
	
	> param.social icon can be searched at [https://fontawesome.com/icons](https://fontawesome.com/icons) and set only the icon part, and other sites can be used.

## 3. Upload changes to your Github repository
1. Hugo build. 
	```sh
	# directory : <Blog repository name>
	$ hugo
	```

2. Upload `<username>.github.io` repository and `<Blog repository name>` repository.

	```sh
	$ cd public
	$ git add .
	$ git commit -m "<commit-message>"
	$ git push origin master
	$ cd ..
	$ git add .
	$ git commit -m "<commit-message>"
	$ git push origin master
	```
	
3. Check github repository.
