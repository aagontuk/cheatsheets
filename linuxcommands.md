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

### Taking Screenshots ###

* Using imagemagick. Issuing this command will change the cusrsor to select a rectagular area. If clicked rather than selecting area entire active window will be captured. Image format will be guessed from the extension provided with the image name.

```
$ import NAME
```
