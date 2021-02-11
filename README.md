# Create-Custom-Maker-Map
How to create a custom-shaped bitmap marker with Android map API 

![Screenshot 2021-02-11 130102](https://user-images.githubusercontent.com/41232970/107628398-3dda1380-6c69-11eb-9b70-de03637a2552.png)
<br />

  ```groovy
   dependencies {

     implementation 'com.rishabhharit.roundedimageview:RoundedImageView:0.8.4'
     implementation 'com.github.bumptech.glide:glide:4.11.0'
     annotationProcessor 'com.github.bumptech.glide:compiler:4.11.0'

     }
  ```
 <br />
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
# 3-Activity or Fragment  .Java or .kt
 ```groovy
   public class SelectDeliveryFragment extends Fragment{
       private ImageView mMarkerImageView;
       private View mCustomMarkerView;

        @Override
      public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
           super.onViewCreated(view, savedInstanceState);
           mCustomMarkerView = ((LayoutInflater) requireActivity().getSystemService(
                   Context.LAYOUT_INFLATER_SERVICE)).inflate(R.layout.view_custom_marker, null);
           mMarkerImageView = (ImageView) mCustomMarkerView.findViewById(R.id.profile_image);
      }
      
       private void addMarkersUser(double lat, double lng, String image) {
          endLatLng = new LatLng(lat, lng);
          usersMarker = mMap.addMarker(new MarkerOptions()
                  .position(endLatLng)
                  .title(notification.getUsers().getNameRes() + " is Here"));
          provideImage(usersMarker, image);

          mMap.moveCamera(CameraUpdateFactory.newLatLng(endLatLng));
          mMap.setOnMarkerClickListener(this);
    }
    
       private void provideImage(Marker marker, String image) {
           Glide.with(requireContext())
                   .asBitmap()
                   .load(image)
                   .fitCenter()
                   .into(new CustomTarget<Bitmap>() {
                       @Override
                       public void onResourceReady(@NonNull Bitmap resource, @Nullable Transition<? super Bitmap> transition) {
                           marker.setIcon(BitmapDescriptorFactory.fromBitmap(getMarkerBitmapFromView(mCustomMarkerView, resource)));
                       }

                       @Override
                       public void onLoadCleared(@Nullable Drawable placeholder) {

                       }
                   });
       }
       
       
        private Bitmap getMarkerBitmapFromView(View view, Bitmap bitmap) {
            mMarkerImageView.setImageBitmap(bitmap);
            view.measure(View.MeasureSpec.UNSPECIFIED, View.MeasureSpec.UNSPECIFIED);
            view.layout(0, 0, view.getMeasuredWidth(), view.getMeasuredHeight());
            view.buildDrawingCache();
            Bitmap returnedBitmap = Bitmap.createBitmap(view.getMeasuredWidth(), view.getMeasuredHeight(),
                    Bitmap.Config.ARGB_8888);
            Canvas canvas = new Canvas(returnedBitmap);
            canvas.drawColor(Color.WHITE, PorterDuff.Mode.SRC_IN);
            Drawable drawable = view.getBackground();
            if (drawable != null)
                drawable.draw(canvas);
            view.draw(canvas);
            return returnedBitmap;
    }
    
   }
```



