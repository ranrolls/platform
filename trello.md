# Harvest and Trello Integration

The Harvest platform enables any web developer to bring time tracking into their application in less than an hour. 
The completed integration is not only easy to implement, it achieves a very seamless integration experience 
for the end-user. A Trello user will be able to track time to a Trello card. 

* Watch a demo: http://www.youtube.com/watch?v=3XvwvhWirU0
* You can also create a free Harvest trial for testing: https://www.getharvest.com/signup

Integrating requires just 3 simple steps.

### 1. Include the Harvest Platform JS Block

Loading the platform requires that the following block and configuration be
specified. Note that we've set two key variables to for Trello, namely "applicationName" and "permalink" (which enables Harvest to link back to Trello)

```html
<script>
  (function() {
    window._harvestPlatformConfig = {
      "applicationName": "Trello",
      "permalink": "https://trello.com/card/%PROJECT_ID%/%ITEM_ID%",
      "skipStyling": true
    };
    var s = document.createElement("script");
    s.src = "https://platform.harvestapp.com/javascripts/generated/platform.js";
    s.async = true;
    var ph = document.getElementsByTagName("script")[0];
    ph.parentNode.insertBefore(s, ph);
  })();
</script>
```

### 2. Add a Harvest "Track time..." button to the Trello card

The Harvest timer is likely best rendered in the Actions list. This can
be accomplished by adding the following markup to the list.

```html
<a class="harvest-timer button-link js-add-trello-timer"
  data-project='{"id": boardId, "name": boardName}'
  data-item='{"id": cardId, "name": cardDescription}'>
  <span class="trello-timer-icon"></span>
  Track time...
</a>
```

### 3. Load supporting CSS

The following styles should be loaded on pages where the "Track time..." buttons are used. 

The button itself is styled differently when its timer is running. This style
matches the one Trello uses for `mouseenter` events.

```css
.js-add-trello-timer.running {
  background: #2887bd;
  background: -moz-linear-gradient(top, #2887bd 0%, #1f6993 100%);
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0%, #2887bd), color-stop(100%, #1f6993));
  background: -webkit-linear-gradient(top, #2887bd 0%, #1f6993 100%);
  background: -o-linear-gradient(top, #2887bd 0%, #1f6993 100%);
  background: -ms-linear-gradient(top, #2887bd 0%, #1f6993 100%);
  background: linear-gradient(top, #2887bd 0%, #1f6993 100%);
  color: white;
}
```

The following styles are used for changing the Harvest timer icon based on the
state of its button.

```css
.trello-timer-icon {
  background-image: url(https://platform.harvestapp.com/images/platform/trello-timer-icon.png);
  background-repeat: no-repeat;
  background-position: 4px -83px;
  display: inline-block;
  position: relative;
  height: 18px;
  width: 18px;
  margin: 0 0 -3px 0;
}

.trello-timer-icon.hover, .trello-timer-icon.running {
  background-position: 4px -122px;
}
```