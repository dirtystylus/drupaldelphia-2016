build-lists: true

# A Story: Content Management the Hard Way

* Native American Voices exhibit at the Penn Museum
* Hundreds of artifacts (~400)
* Content management with static XML and local files

---

![inline](./images/ice-climbing.gif)

#### *[littlepawz.tumblr.com](http://littlepawz.tumblr.com/post/113859078234/lifes-oh-sht-moment-44)*

---

> XML is not meant to be hand-authored. It’s an output artifact.
-- A smarter person than me

---

# Connecting the Dots

* Web stuff over here, lots of CMS/website builds
* Applications over there (iOS, Android, Cinder)

---

# [fit] Pain = signal

---

# Start Small

* We built a CMS using something that rhymes with “bird dress”
* JSON, not XML
* Preprocessing, not “live”

---

# Case Study: Field Museum

![inline fill](./images/52377145_d31c18f161_b.jpg)

#### [David Thompson (https://www.flickr.com/photos/39023889@N00/52377145)](https://www.flickr.com/photos/39023889@N00/52377145)

---

# Case Study: Field Museum

* Digital Orientation Screens for finding out information on Exhibits, Events, Amenities
* Twelve 55" screens throughout the Museum
* Client team was familiar with Drupal, so we looked into what we could do with Drupal

---

# Video

![inline](./videos/field-dos.mp4)

---

# Case Study: Field Museum

* Drupal 7, Services module plus Services Views
* Screens needed to download content locally in case of network outage. Used bash scripts to rsync JSON and images from server to local network.
* Custom module to “mark” feeds that needed updating (you’d probably use a nodejs server for this instead)
* Twilio for SMS message with link to custom map
* Custom module to render map
