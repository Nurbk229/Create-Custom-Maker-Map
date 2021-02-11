# Create-Custom-Maker-Map
How to create a custom-shaped bitmap marker with Android map API 

![Screenshot 2021-02-11 130102](https://user-images.githubusercontent.com/41232970/107628398-3dda1380-6c69-11eb-9b70-de03637a2552.png)


 ```groovy
dependencies {
  implementation 'com.rishabhharit.roundedimageview:RoundedImageView:0.8.4'
  }
 ```
 <br /><br /><br />
 # 1-Layout
 view_custom_marker.xml
 ```groovy 
  <?xml version="1.0" encoding="utf-8"?>
  <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"
      android:id="@+id/custom_marker_view"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content">

      <ImageView
          android:layout_width="30dp"
          android:layout_height="48dp"
          android:layout_gravity="center_horizontal"
          android:layout_marginTop="17dp"
          android:background="@drawable/ic_marker"
          android:scaleX="1" />

      <com.rishabhharit.roundedimageview.RoundedImageView
          android:layout_width="48dp"
          android:layout_height="48dp"
          app:cornerRadius="1000dp"
          app:roundedCorners="all"
          android:src="@color/colorOrange" />

      <com.rishabhharit.roundedimageview.RoundedImageView
          android:id="@+id/profile_image"
          android:layout_width="44dp"
          android:layout_marginTop="2dp"
          android:layout_height="44dp"
          android:scaleType="centerCrop"
          app:cornerRadius="1000dp"
          app:roundedCorners="all"
          android:layout_gravity="center_horizontal"
          android:contentDescription="@null"
          android:padding="4dp" />

  </FrameLayout>
```
<br /> <br /> <br />
# 2-drawable
ic_marker.png<br />
![ic_marker](https://user-images.githubusercontent.com/41232970/107628840-e5efdc80-6c69-11eb-82c8-dc92b03ed0cb.png)

<br /> <br /> <br />
Activity or Fragment  .Java or .kt




