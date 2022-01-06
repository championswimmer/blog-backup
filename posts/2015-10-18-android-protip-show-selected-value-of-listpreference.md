---
title: "Android Protip: Show selected value of ListPreference"
slug: android-protip-show-selected-value-of-listpreference
date_published: 2015-10-18T00:00:00.000Z
date_updated: 2015-10-18T00:00:00.000Z
---

Here's a quick Protip for people who are still writing complex `onPreferenceChanged` code to show the selected value of a *ListPreference*

Just add `android:summary="%s"` and Android will automatically do it for you ;)

For example, your code might look like : -

        <ListPreference
            android:summary="%s"
            android:defaultValue="km"
            android:entries="@array/distance_unit_names"
            android:entryValues="@array/distance_unit_values"
            android:key="distance_unit"
            android:title="Distance Unit"/>
    
    

Android will even put the currently selected value when you enter the preference screen.
