
# github.io 구축 (hugo-coder 테마 사용)
> [English : github.io by using hugo-coder theme](https://github.com/ClaudiaJKang/ClaudiaJKang.github.io/blob/master/README.md)

## 1. Hugo 설치 
1. go 설치.
	```bash
	# fedora31 기준 
	$ sudo dnf install golang
	$ mkdir -p $HOME/go
	$ echo 'export GOPATH=$HOME/go' >> $HOME/.bashrc
	$ source $HOME/.bashrc
	```
	> [go 설치 페도라 문서](https://developer.fedoraproject.org/tech/languages/go/go-installation.html)

2. Hugo 설치.
	```bash
	# github repo 설치 기준
	$ cd  $HOME/go/pkg
	$ git clone https://github.com/gohugoio/hugo.git 
	$ cd hugo 
	$ go install --tags extended
	$ sudo su
	$ cd /usr/bin
	$ ln -s $HOME/go/bin/hugo hugo
	```
	> [Hugo 설치 공식 문서](https://gohugo.io/getting-started/installing/#fetch-from-github)

## 2. Hugo-coder 테마 설정
1. 사용 할 [hugo-coder](https://github.com/luizdepra/hugo-coder) 테마 Github 레포지토리를 fork. 
2. `<Blog repository name>`, `<username>.github.io` Github 레포지토리 생성. 
3. 새로운 사이트 생성
	```bash
	$ hugo new site <Blog repository name> # 2번의 <Blog repository name>과 동일
	```
4. git remote 추가
	```bash
	$ cd <Blog repository name>
	$ git init
	$ git remote add origin https://github.com/<username>/<Blog repository name>.git
	$ git fetch origin
	```

5. themes git submodule 추가 
	```bash
	$ git submodule add https://github.com/<username>/hugo-coder themes/hugo-coder
	```

6. public git submodule 추가
	```bash
	$ git submodule add https//github.com/<username>/<Blog repository name> public
	```

7. Hugo build
	```bash
	# <Blog repository name> 폴더에서 명령 입력
	$ hugo
	```

8. css 파일명 확인
	```bash
	$ ls public/css
	<css file name>.css
	```

9. config.toml 파일 설정
	```bash
	baseurl = "https://<github.io 주소>"
	title = "<Blog 이름>"
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
	    author = "<이름>"
	    info = "<경력 정보>"
	    description = "<Blog 설명>"
	    keywords = "blog,developer,personal"
	    avatarurl = "<사진 url>"

	    favicon_32 = "/img/favicon-32x32.png"
	    favicon_16 = "/img/favicon-16x16.png"

	    hidecredits = false
	    hidecopyright = false

	    rtl = false

	    math = true
	    custom_css = ["css/<8번 css 파일명>"]

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

	> [hugo-coder exampleSite config.toml 파일 참고](https://github.com/luizdepra/hugo-coder/blob/master/exampleSite/config.toml) 
	
	> [hugo-coder config.toml 구성 설명 문서](https://github.com/luizdepra/hugo-coder/wiki/Configurations)
	
	> param.social icon은 [https://fontawesome.com/icons](https://fontawesome.com/icons)에서 검색해서 icon 부분만 설정해주면 다른 사이트도 가능

## 3. Github 레포지토리에 변동사항 업로드
1. hugo build 
	```bash
	# <Blog repository name> 폴더에서 명령 입력
	$ hugo
	```

2. `<username>.github.io 레포지토리` 및 `<Blog repository name> 레포지토리`에 업로드
	```bash
	$ cd public
	$ git add .
	$ git commit -m "<commit-message>"
	$ git push origin master
	$ cd ..
	$ git add .
	$ git commit -m "<commit-message>"
	$ git push origin master
	```

3. 변동사항 github 레포지토리에서 확인
