# PhotoSwipe plugin

A plugin for [Kirby 3 CMS](http://getkirby.com) that adds [photoswipe](http://photoswipe.com/) v5 Beta.

## Commercial Usage

This plugin is free but if you use it in a commercial project please consider

- [making a donation](https://www.paypal.me/schnti/5) or
- [buying a Kirby license using this affiliate link](https://a.paddle.com/v2/click/1129/48194?link=1170)

## Installation

### Download

[Download the files](https://github.com/schnti/kirby3-photoswipe/archive/master.zip) and place them inside `site/plugins/photoswipe`.

### Git Submodule

You can add the plugin as a Git submodule.

    $ cd your/project/root
    $ git submodule add https://github.com/schnti/kirby3-photoswipe.git site/plugins/photoswipe
    $ git submodule update --init --recursive
    $ git commit -am "Add Kirby PhotoSwipe plugin"

Run these commands to update the plugin:

    $ cd your/project/root
    $ git submodule foreach git checkout master
    $ git submodule foreach git pull
    $ git commit -am "Update submodules"
    $ git submodule update --init --recursive

### Composer

```
composer require schnti/photoswipe
```

### Install PhotoSwipe

```
npm install --save git://github.com/dimsemenov/photoswipe#v5-beta
```

#### JS
```
import PhotoSwipeLightbox from 'photoswipe/dist/photoswipe-lightbox.esm.js';
import PhotoSwipe from 'photoswipe/dist/photoswipe.esm.js';

// don't forget to include CSS in some way
// import 'photoswipe/dist/photoswipe.css';

const lightbox = new PhotoSwipeLightbox({
  gallery: '.photoswipe',
  children: 'a',
  pswpModule: PhotoSwipe
});
lightbox.init();

```

#### CSS/SCSS
```
@import "~photoswipe/src/photoswipe.css";
```

### Add static gallery

```
<div class="photoswipe">
    <figure>
        <a href="large-image.jpg" data-pswp-width="800" data-pswp-height="600" target="_blank">
            <img src="small-image.jpg" alt="Image description" />
        </a>
        <figcaption>Image caption</figcaption>
    </figure>
</div>
```

### or add dynamic gallery with kirby markup (and [Bootstrap 5](https://getbootstrap.com/docs) Grid)

```
<div class="row photoswipe">
    <?php foreach ($page->images() as $image): ?>

        <?php $pic = $image->resize(2000, null, 90); ?>

        <figure class="col-4">
            <a href="<?= $pic->url(); ?>"
               data-pswp-width="<?= $pic->width(); ?>"
               data-pswp-height="<?= $pic->height(); ?>"
               title="<?= $image->text()->value(); ?>"
               target="_blank">
                <img class="img-fluid" src="<?= $image->crop(600, 380, 80)->url(); ?>" alt="<?= $page->title()->value() ?> <?= $image->text()->value(); ?>"/>
            </a>

            <figcaption><?= $image->alt()->kirbytextinline() ?></figcaption>
        </figure>

    <?php endforeach; ?>
</div>
```

### or use the photoswipe kirbytag

```
(photoswipe: image.jpg
    width: 200
    height: 200
    quality: 70
    crop: true
)
```

#### Tag Attributes

**Thumbnail**

* **width**: Integer (thumbnail resize width, default: 300)
* **height**: Integer (thumbnail resize height, default: null)
* **quality**: Integer (jpeg quality from 0 to 100, default: 70)
* **crop**: Boolean (enable cropping the file according to the given width and height parameters, default: false)

**Image**

* **pwidth**: Integer (image resize widt, default: 1000)
* **pheight**: Integer (image resize height, default: null)
* **pquality**: Integer (jpeg quality from 0 to 100, default: 80)