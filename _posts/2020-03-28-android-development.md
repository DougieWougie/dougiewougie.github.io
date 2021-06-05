---
layout: post
author: Dougie
category: programming
---

Having not developed anything in Java since finishing university, opening Android Studio seemed like looking at an alien language. While I'd love to say it all came flooding back, that wouldn't be true. Downloading the source to my last app from GitHub really didn't help either.
<!-- more -->
Time for another self-help guide.

Android uses the Model View Controller (MVC) design paradigm, where the controller is the device's sensors and screen. The model is Java or Kotlin contained in an Activity whereas the view is defined using a Layout described in XML. An Activity is a single defined task on a single screen.

Android Studio generates folder structure and required skeleton files. Localisation is also simplified using string resources using `/res/values/strings.xml`. Entries use the format `<string name="action_settings">Settings</string>` and are accessed within layouts using `android:text="@string/action_settings" />`.

A View is the basic building block of a UI - each UI component has a View Object as it's base class. It occupies a rectuangular space on screen and has getters/setters, an ID, size and position, focus handling and event handlers/listeners. A ViewGroup Object combines Views using a layout to form a UI. Each View is defined in the layout:

    <Button
        android:id="@+id/button"
        android:onClick="onButtonClicked" />

In the Java Activity (note the View object being passed):

    /** Called when the button is clicked */
    public void onButtonClicked(View view) {
        ...
    }

Setting or a View property, such as a TextView's Text:

    TextView textView = (TextView) findViewById(R.id.text_view);
    textView.setText("New  text");

# Life cycle
Android apps have a life cycle and there are methods called on state change.
