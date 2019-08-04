### User Administration ###

#### Adding a user to a group ####

```
$ usermod -a -G GROUP USER  # Add USER to GROUP
```

### Image manipulation ###

#### Converting image formats ####

* Using imageMagick. Image format is guessed from the extension. You can also specify new image height and width.

```
$ convert FROM_IMG TO_IMAGE
```

* Using inkscape. Gives better result than imageMagic for SVG image formats

```
$ inkscape -z -e TO_IMAGE FROM_IMAGE
```
