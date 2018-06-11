---
layout: post
title: Automatisch, zentriertes Zuschneiden des Featured Image bei Wordpress
date: 2016-04-30
tags: [deutsch, technology]
---

Das original Wordpress Theme [Twenty Sixteen](https://wordpress.org/themes/twentysixteen/) verwendet ein [Featured Image](https://codex.wordpress.org/Post_Thumbnails) über jedem Blog Eintrag, wenn auch ein Bild gesetzt wurde. Wer nun zu faul ist dieses Bild vorweg zurechtzuschneiden, damit man nicht ewig zum Text scrollen muss, kann sich die Arbeit von etwas CSS abnehmen lassen.

```css
.post-thumbnail {
    max-height: 200px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.post-thumbnail img {
    flex-shrink: 0;
}
```

Dieser CSS Block schneidet das Bild bei der Anzeige auf 200 Pixel zu, zentriert es jedoch zuvor. Der original Blog Eintrag stimmt von [Jan Dembowski](https://blog.dembowski.net/2015/center-cropping-featured-images-in-css/).