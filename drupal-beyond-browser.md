build-lists: true
autoscale: true


# A Story: Content Management the Hard Way

![inline fit mute](./videos/nav.mp4)

^ Artifacts—images, video, audio

^ Profiles of prominent Native American leaders

^ 15-foot touch towers

^ 12 kiosk touchscreens corresponding to artifact cases

---

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

David Thompson [(https://www.flickr.com/photos/39023889@N00/52377145)](https://www.flickr.com/photos/39023889@N00/52377145)

---

# Case Study: Field Museum

* Digital Orientation Screens for finding out information on Exhibits, Events, Amenities
* Twelve 55" screens throughout the Museum
* Client team was familiar with Drupal, so we looked into what we could do with Drupal

---

![fit](./videos/field-dos.mp4)

---

# Case Study: Field Museum

* Drupal 7, Services module plus Services Views
* Screens needed to download content locally. Used bash scripts to rsync JSON and images from server to local network.

---

## Case Study: Field Museum
### Custom module to “mark” feeds that needed updating

* **TODO**: try nodejs
* App only wanted to sync JSON data/images for new content
* Services Views could create output for the last created/modified node of each type
* **BUT**: Deleting a node would not be reflected

---

## Case Study: Field Museum
### Custom module to “mark” feeds that needed updating

* `hook_node_presave()`
* `hook_node_delete()`
* `hook_taxonomy_term_presave()`
* `hook_taxonomy_term_delete()`

---

### Case Study: Field Museum
#### Custom module to “mark” feeds that needed updating

```php
function field_dos_feed_status_node_presave($node) {
  switch ($node->type) {
    case 'amenity':
      variable_set('amenities_timestamp', time());
      break;
    case 'behind_scenes_item':
      variable_set('behind_scenes_items_timestamp', time());
      break;  
    case 'collection_highlight':
      variable_set('collection_highlights_timestamp', time());
      break;
    case 'exhibit_item':
      variable_set('exhibit_items_timestamp', time());
      break;
    case 'schedule_item':
      variable_set('schedule_items_timestamp', time());
      break;
    case 'touchscreen_station':
      variable_set('touchscreen_stations_timestamp', time());
      break;
    case 'itinerary':
      variable_set('itineraries_timestamp', time());
      break;  
    default:
      break;
  }
}
```

---

### Case Study: Field Museum
#### Custom module to “mark” feeds that needed updating

```php
function field_dos_feed_status_menu_object() {
    $feeds = array(
      array('amenities' => variable_get('amenities_timestamp', '')),
      array('amenity-categories' => variable_get('amenity_categories_timestamp', '')),
      array('behind-the-scenes-items' => variable_get('behind_scenes_items_timestamp', '')),
      array('collection-highlights' => variable_get('collection_highlights_timestamp', '')),
      array('exhibit-items' => variable_get('exhibit_items_timestamp', '')),
      array('itineraries' => variable_get('itineraries_timestamp', '')),
      array('locations' => variable_get('locations_timestamp', '')),
      array('schedule' => variable_get('schedule_items_timestamp', '')),
      array('touchscreen-stations' => variable_get('touchscreen_stations_timestamp', '')),
    );
    return $feeds;
}
```

---

### Case Study: Field Museum
#### Custom module to “mark” feeds that needed updating

```json
[
	{"amenities":1449786054},
	{"amenity-categories":1450716038},
	{"behind-the-scenes-items":1449606828},
	{"collection-highlights":1449607778},
	{"exhibit-items":1451915487},
	{"itineraries":1449608094},
	{"locations":1451915570},
	{"schedule":1454972584},
	{"touchscreen-stations":1439735864}
]
```

---

# Case Study: Field Museum
### Front End

* AngularJS (wait but I thought you said no browsers)
* [TweenMax (http://greensock.com/tweenmax)](http://greensock.com/tweenmax)

---

# Case Study: Field Museum
### Front End

![inline fit](./images/tyrion-eyebrows.gif)

---

# Case Study: Field Museum
### Front End

* Single touch
* Typography in Cinder is still…developing

---

# [fit] Case Study: :ear: :art:

---

# Case Study: Van Gogh’s Bedrooms

* Installation bringing three versions of Van Gogh’s bedroom together
* Projection / touchscreen

---

![fit](./videos/van-gogh.mp4)

---

# Case Study: Van Gogh’s Bedrooms

* CMS originally in WordPress for initial build, client standardized on Drupal so we rebuilt the CMS
* Drupal 7, Services and Services Views to provide JSON
* Cinder (C++) application

---

# D7 Recipe

* D7: Install Services module and Services Views
*  Drupalize.me series: [https://drupalize.me/videos/introduction-building-services-drupal-7-series?p=1487](https://drupalize.me/videos/introduction-building-services-drupal-7-series?p=1487)

---

# D7 Recipe

### Create a View with a Services Display

![inline](./images/d7-services-views.jpg)

---

# D7 Recipe

### Add fields, assign value keys

![inline](./images/d7-value-key.png)

---

# D7 Recipe

### Configure Service

![inline](./images/d7-services.jpg)

---

# D7 Recipe

### Select response formats

![inline](./images/d7-services-server.jpg)

---

# D7 Recipe

### Select resources (Your View)

![inline](./images/d7-services-resources.png)


---

# D7 Recipe

### Output

![inline](./images/d7-services-output.jpg)

---

![105%](./images/drupal-8-potato-1920x1080.jpg)

## Drupal 8
### So what do we get out of the box?


---

## 3 ways to create a REST API with Drupal 8

---

- Option: #1 - _**Using the core Rest Resources**_

- Option: #2 - _**Using View REST exports**_

- Option: #3 - _**Create custom REST endpoint**_

---

![right fit](./images/screenshot-d8-01.png)

##Option: #1 - __*Using the core Rest Resources*__

```php
/node/{node}
/entity/node_type/{node_type}
/entity/block/{block}
/comment/{comment}
/entity/comment_type/{comment_type}
```
---
![140% filtered](./images/drupal_2_1920x1080_widescreen.jpg)

#Demo
### Option #1

---

#Pros
- Straight out of the box
- Requires almost no setup
- No custom code necessary

#Cons
- Absolutely no ﬂexibility
- Lacks ability to version
- Unable to limit output. Using the core REST resources

---

![right fit](./images/screenshot-d8-02.png)

##Option: #2 - __*Using View REST exports*__
- Views is now in core and also comes bundled with REST support out of the box.

---
![140%](./images/drupal_2_1920x1080_widescreen.jpg)

#Demo
### Option #2

---

#Pros
- Straight out of the box
- Familiar to developers
- Manageable within the UI

#Cons
- Returns data with incorrect types
- More ﬂexibility, but still limited in various areas
- No ways to set custom parameters
- Authentication issues. Using views REST export

---

##Option: #3 - __*Create custom REST endpoint*__

---

#Pros
- Provides most ﬂexibility
- Transformable output
- Easier to manage versions

#Cons
- Requires reasonable programming knowledge

---

# Power of Decoupled Architectures

* Content management can stay stable
* (Multiple) frontends can change. Prototype in one language, build in another.
* Barrier to entry is low

### ---