# pHTellerApp
Mobile all that uses machine learning model to show the precise pH value of pH strip.
Why Machine Learning for pH Finding: Generally pH strip is used to find the pH value of a chemical but for some pH value of like 4,5 and 8,9 etc it is very difficult to find out the color difference by manual observation. To solve this issue machine learning is integrated here. I have trained the ML model with 439 labelled data of pH 1 to pH 13. Take the picture of ph strip after dipping into a solution and then take the picture from the this app (as of now crop feature is not available I'll add that later on). This app will Tell you the exact pH value(as of now model is trained for integer value only). This is a working project so I will keep on update here if any new feature is added into the app.


This is how app look like:

![image](https://github.com/meHypernova/pHTellerApp/assets/146374681/c30a4a55-1af0-4d67-af18-b05eee018db2)


XML File of the app:

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/bg"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/rgb_value"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="1dp"
        android:layout_marginEnd="1dp"
        android:gravity="center"
        android:hint="@string/rgb_value"
        android:textColorHint="#000000"
        app:layout_constraintBottom_toTopOf="@+id/pHOut"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/CameraPic" />

    <TextView
        android:id="@+id/pHOut"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="4dp"
        android:layout_marginEnd="4dp"
        android:layout_marginBottom="15dp"
        android:gravity="center"
        android:hint="@string/pHOut"
        android:textColorHint="#000000"
        app:layout_constraintBottom_toTopOf="@+id/predictButton"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/rgb_value" />

    <Button
        android:id="@+id/gallery"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="9dp"
        android:layout_marginEnd="14dp"
        android:text="@string/gallery"
        android:textSize="15dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/Camerabtn"
        app:layout_constraintTop_toBottomOf="@+id/predictButton" />

    <Button
        android:id="@+id/Camerabtn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="20dp"
        android:layout_marginBottom="13dp"
        android:text="@string/OpenC"
        android:textSize="15dp"
        app:layout_constraintBottom_toTopOf="@+id/textView"
        app:layout_constraintEnd_toStartOf="@+id/gallery"
        app:layout_constraintHorizontal_chainStyle="packed"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/predictButton" />

    <Button
        android:id="@+id/predictButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="9dp"
        android:text="@string/predictbtn"
        app:layout_constraintBottom_toTopOf="@+id/Camerabtn"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/pHOut" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/wel"
        android:textColor="@color/black"
        android:textSize="10dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/Camerabtn" />

    <ImageView
        android:id="@+id/CameraPic"
        android:layout_width="416dp"
        android:layout_height="470dp"
        android:layout_marginBottom="6dp"
        android:background="@drawable/img"
        android:scaleType="fitXY"
        android:src="#11000000"
        app:layout_constraintBottom_toTopOf="@+id/rgb_value"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>


Main Activity File


protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnGallery = findViewById(R.id.gallery);
        imageView = findViewById(R.id.CameraPic);
        pHValueOutput = findViewById(R.id.pHOut);
        RGBValue = findViewById(R.id.rgb_value);
        btnCamera = findViewById(R.id.Camerabtn);
        PreditButton = findViewById(R.id.predictButton);

        btnCamera.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                dispatchTakePictureIntent();
            }
        });

        btnGallery.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                openGallery();
            }
        });

        PreditButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (currentImageBitmap != null) {
                    processAndSendImage(currentImageBitmap);
                } else {
                    Toast.makeText(getApplicationContext(), "Please select an image first.", Toast.LENGTH_SHORT).show();
                }
            }
        });
    }


    //This app is a part of my MTP so I can't share the whole code as of now.


