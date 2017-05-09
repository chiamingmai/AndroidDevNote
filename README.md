# AndroidDevNote
A note for developing Android Apps

---
### **Use vector drawables on older platforms (< 21)**

1. In older paltforms, the `Resources$NotFoundException` error will show up while getting the vector drawables.
   
   Do the following steps to fix this.
   - Call this line in Activity before getting the drawables,
    ```Java
    AppCompatDelegate.setCompatVectorFromResourcesEnabled(true);
    ```
   - then call one of these lines to get drawables.
    ```java
    android.support.v4.content.ContextCompat.getDrawable(Context context, @DrawableRes int id);
    ```

    ```Java
    android.support.v4.content.res.ResourcesCompat.getDrawable(Resources res, @DrawableRes int id, Theme theme);
    ```
    
2. Use VectorDrawableCompat to get vector graphics.
    ```java
    android.support.graphics.drawable.VectorDrawableCompat.create(@NonNull Resources res,
        @DrawableRes int resId, @Nullable Theme theme);
    ```

### **Change vector drawable's color**

1. In xml:
    - Create color selector (state_selector.xml) in `res/color` directory.
    ```xml
      <selector xmlns:android="http://schemas.android.com/apk/res/android">
        <item android:color="@color/itemSelected" android:state_selected="true" />
        <item android:color="@color/itemUnselected" android:state_selected="false" />
      </selector>
    ```
    - add "state_selector" to "android:tint" attribute in vector drawable.
    ```xml
    <vector xmlns:android="http://schemas.android.com/apk/res/android"
        android:width="24dp"
        android:height="24dp"
        android:viewportWidth="24.0"
        android:viewportHeight="24.0"
        android:tint="@color/state_selector" > /*use selector in this line*/
        
            <path
            android:fillColor="#FF000000"
            android:pathData="M19,3h-4.18....." />
    </vector>
    ````

2. In code:
    
    call setColorFilter, this also works in 21 lower platforms.
    ```java
    Drawable.setColorFilter(@ColorInt int color, @NonNull PorterDuff.Mode mode);
    ```
    or call setTint, this works on 21 and higher platforms.
    ```java
    Drawable.setTint(@ColorInt int tintColor);
    ```


