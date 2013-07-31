Project website
==================

The project website is build using awestruct with markdown. A further version might use asciidocter instead.

## Run

rake clean preview

localhost:4242

## Deploy

awestruct -P production --force -g --deploy
