# Get started Hexo

- homepage: [https://hexo.io/](https://hexo.io/)
- github: [https://github.com/hexojs/hexo](https://github.com/hexojs/hexo)

## Install Hexo

    $ npm install hexo-cli -g

If got this error:

    npm WARN checkPermissions Missing write access to /usr/local/lib/node_modules

set permission to this path:

    $ sudo chown -R $USER /usr/local/lib/node_modules

## Setup to launch

    $ hexo init blog
    $ cd blog
    $ npm install
    $ hexo server            // launch the hexo server

## Install hexo-deployer-git and configure

install hexo-deployer-git

    $ npm install hexo-deployer-git --save

and modify configure file `_config.yml` for deploy to github

    # Extensions
    ## Plugins: https://hexo.io/plugins/
    plugins: hexo-deployer-git
    
    # Deployment
    ## Docs: https://hexo.io/docs/deployment.html
    deploy:
      type: git
      repo: [github repository url]
      branch: master
      name: [github user name]
      email: [github user email]

can configure gitconfig in `.deploy_git/.git/config`
