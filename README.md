## Getting Started

    $ brew install rbenv
    $ rbenv init # make sure your shell is setup
    $ rbenv install -l # install the lastest
    $ rbenv global $(rbenv versions --bare | tail -1) # set latest as global version
    $ gem install jekyll jekyll-paginate
    $ jekyll serve --drafts --incremental