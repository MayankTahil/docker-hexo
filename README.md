# docker-hexo

A Docker Container for [Hexo](http://hexo.io/).

[docker-hexo](https://github.com/mayankt/docker-hexo) image based on [node:alpine](https://hub.docker.com/_/node/), pandoc is optional for processing markdown files with better MathJax support and enhanced markdown such as footnotes.

## Use example  

For ease of use, you can set alias/bash-functions for tedious docker command in `~/.bashrc` or `~/.zshenv`. Be sure your current user are in `docker` group.

```bash
# Hexo Blog
hexo(){
	if [ "$1" = "npm" ]; then
		string=""
    for a in "$@" # Loop over arguments
    do
      string+=" " # Delimeter
      string+="$a"
    done
  	docker run --rm -v "$PWD:/blog" -p 4000:4000 mayankt/hexo-cli npm $string
  else
		string=""
    for a in "$@" # Loop over arguments
    do
      if [[ "$string" != "" ]]
      then
          string+=" " # Delimeter
      fi
      string+="$a"
    done
  	docker run --rm -v "$PWD:/blog" -p 4000:4000 mayankt/hexo-cli hexo $string
  fi
}
```

Use `hexo npm install` for `npm install ...`, and `hexo` for `hexo ...` commands.

### Example  

```
hexo init <folder>
cd <folder>
hexo npm install
```

## Install Hexo plugins  

Various plugins can be found on [Plugins · hexojs/hexo Wiki](https://github.com/hexojs/hexo/wiki/plugins), replace `npm` with `hexo npm`. :)
