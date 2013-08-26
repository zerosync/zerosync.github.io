Project website
==================

The project website is build using awestruct with asciidoctor.

## Install under Ubuntu

* Install prerequisites 

`apt-get install ruby-dev libxml2-dev libxslt-dev rake`

* Install gems

`gem install awestruct bundler asciidoctor`


## Run in development mode

`rake clean preview`

View the compiled website in the browser http://localhost:4242

## Deploy to production

`awestruct -P production --force -g --deploy`
