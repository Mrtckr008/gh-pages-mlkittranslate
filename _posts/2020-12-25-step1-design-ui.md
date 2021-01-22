---
title: "Step 2: Add activity_translate.xml"
description: 5
---

##### Designing the UI

1. We will write a sentence in any supported language according to the scenario. We will be able to choose which language this sentence will be translated into. We will do this using Spinner. There will also be a translate button. With this button, we will run the translation process and show it to the user. In this codelab, you can create the UI in your Android Studio project, by referring to the following UI layout.

   
       <?xml version="1.0" encoding="utf-8"?>
       <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
           xmlns:app="http://schemas.android.com/apk/res-auto"
           xmlns:tools="http://schemas.android.com/tools"
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           android:background="#E4E4E4"
           tools:context=".TranslateActivity">
       <EditText
           android:id="@+id/translate_edittext"
           android:layout_width="0dp"
           android:layout_height="200dp"
           android:layout_marginStart="8dp"
           android:layout_marginEnd="8dp"
           android:background="#FFFFFF"
           android:ems="10"
           android:gravity="clip_horizontal"
           android:hint="Write any language here"
           android:inputType="textMultiLine|textPersonName"
           android:padding="8dp"
           android:singleLine="false"
           app:layout_constraintEnd_toEndOf="parent"
           app:layout_constraintStart_toStartOf="parent"
           app:layout_constraintTop_toBottomOf="@+id/detect_language_text" />
       
       <TextView
           android:id="@+id/detect_language_text"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="Detect Language"
           android:textSize="18sp"
           app:layout_constraintEnd_toEndOf="parent"
           app:layout_constraintStart_toStartOf="parent"
           app:layout_constraintTop_toTopOf="parent" />
       
       <TextView
           android:id="@+id/translation_text"
           android:layout_width="0dp"
           android:layout_height="200dp"
           android:layout_marginTop="8dp"
           android:background="#FFFFFF"
           android:padding="8dp"
           android:text="Translation"
           android:textSize="18sp"
           app:layout_constraintEnd_toEndOf="@+id/translate_edittext"
           app:layout_constraintHorizontal_bias="0.0"
           app:layout_constraintStart_toStartOf="@+id/translate_edittext"
           app:layout_constraintTop_toBottomOf="@+id/language_spinner" />
       
       <Spinner
           android:id="@+id/language_spinner"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_marginTop="16dp"
           app:layout_constraintEnd_toEndOf="parent"
           app:layout_constraintTop_toBottomOf="@id/translate_edittext" />
       
       <TextView
           android:id="@+id/translation_language_text"
           android:layout_width="0dp"
           android:layout_height="wrap_content"
           android:background="#FFFFFF"
           android:text="French"
           app:layout_constraintBottom_toBottomOf="@+id/language_spinner"
           app:layout_constraintEnd_toStartOf="@+id/language_spinner"
           app:layout_constraintStart_toStartOf="@+id/translation_text"
           app:layout_constraintTop_toTopOf="@+id/language_spinner" />
       
       <Button
           android:id="@+id/translate_button"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_marginTop="8dp"
           android:text="Translate"
           app:layout_constraintEnd_toEndOf="parent"
           app:layout_constraintStart_toStartOf="parent"
           app:layout_constraintTop_toBottomOf="@+id/translation_text" />
       </androidx.constraintlayout.widget.ConstraintLayout>

![ss_ui_design](C:\Users\m00565027\Desktop\gh-pages-locationkitcodelab-main\assets\ss_ui_design.png)