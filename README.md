# UTS PEMROGRAMAN MOBILE
# NIM : 312210344
# KELAS : TI.22.A3


## Soal

<img width="400" alt="soal" src="https://github.com/twn304/UTS_Mobile/assets/115573041/039422bc-d9e7-48ea-ab2a-3156224bddcc">

## Input
* ```AndroidManifest.xml```
```python
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.HelloToast"
        tools:targetApi="31">
        <activity
            android:name=".MainToast"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```
* ```MainToast.java```
```java
package com.hellotoast;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;
import android.widget.EditText;
public class MainToast extends AppCompatActivity {
    private int hitung = 1;
    private TextView showHitung;
    private int fib1 = 1;
    private int fib2 = 1;
    private EditText inputCount;
    private boolean maxCountSet = false;
    private int maxCount = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_toast);
        showHitung = (TextView) findViewById(R.id.show_count);
        inputCount = (EditText) findViewById(R.id.max_input);
        fib1 = 1;
        fib2 = 1;
        showHitung.setText(Integer.toString(fib1));
    }

    public void showtoast(View view) {
        Toast toast = Toast.makeText(this, R.string.toast_message, Toast.LENGTH_SHORT);
        toast.show();
        showHitung.setText(Integer.toString(1));
    }

    public void toBack(View view) {
        fib1 = 1;
        fib2 = 1;
        maxCount = 0;
        maxCountSet = false;
        inputCount.setText("");
        showHitung.setText(Integer.toString(0));
    }

    public void setMaxCount(View view) {
        String maxCountString = inputCount.getText().toString();
        if (!maxCountString.isEmpty()) {
            int newMaxCount = Integer.parseInt(maxCountString);
            if (newMaxCount >= 0) {
                maxCount = newMaxCount;
            }
        }
    }
    public void countUp(View view) {
        String maxCountString = inputCount.getText().toString();

        if (!maxCountString.isEmpty()) {
            int maxCount = Integer.parseInt(maxCountString);
            int nextFib = fib1 + fib2;

            if (maxCount >= 0) {
                if (fib1 <= maxCount) {
                    if (nextFib <= maxCount) {
                        fib1 = nextFib;
                        int temp = fib1;
                        fib1 = fib2;
                        fib2 = nextFib;
                    } else {
                        fib2 = fib2;
                    }
                    showHitung.setText(Integer.toString(fib2));
                } else {
                    fib1 = 1;
                    fib2 = 1;
                    showHitung.setText(Integer.toString(0));
                }
            }
        } else {
            int nextFib = fib1 + fib2;
            fib1 = fib2;
            fib2 = nextFib;
            showHitung.setText(Integer.toString(fib1));
        }
    }
}
```
* ```activity_toast.xml```
```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFEB3B"
    tools:context=".MainToast">


    <TextView
        android:id="@+id/show_count"
        android:layout_width="414dp"
        android:layout_height="800dp"
        android:background="#FFFF00"
        android:gravity="center"
        android:text="@string/count_initial_value"
        android:textAlignment="center"
        android:textSize="160sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintHorizontal_bias="0.666"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.507" />

    <Button
        android:id="@+id/set_max_button"
        android:layout_width="153dp"
        android:layout_height="56dp"
        android:layout_below="@id/max_input"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="4dp"
        android:onClick="setMaxCount"
        android:text="Set Max Count"

        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.025"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/button_count"
        android:layout_width="200dp"
        android:layout_height="50dp"
        android:layout_marginBottom="0dp"
        android:background="@color/design_default_color_primary"
        android:backgroundTint="@color/design_default_color_primary"
        android:onClick="countUp"
        android:text="@string/button_label_count"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/button_back"
        android:layout_width="200dp"
        android:layout_height="50dp"
        android:background="@color/design_default_color_primary"
        android:backgroundTint="@color/design_default_color_primary"
        android:onClick="toBack"
        android:text="@string/button_label_back"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent" />

    <EditText
        android:id="@+id/max_input"
        android:layout_width="221dp"
        android:layout_height="62dp"
        android:background="#FFFF00"
        android:hint="Enter maximum input"
        android:inputType="number"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toEndOf="@+id/set_max_button"
        app:layout_constraintTop_toBottomOf="@id/show_count"
        app:layout_constraintTop_toTopOf="parent" />


</androidx.constraintlayout.widget.ConstraintLayout>
```
* ```Color.xml```
```python
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="blue">#0000FF</color>
    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
</resources>
```
* ```string.xml```
```xml
<resources>
    <string name="app_name">Hello Toast</string>
    <string name="halo">Bagaimana Kabar Anda Hari Ini!</string>
    <string name="button_label_toast">Toast</string>
    <string name="button_label_count">Count</string>
    <string name="button_label_back">Back</string>
    <string name="count_initial_value">0</string>
    <string name="toast_message">Button</string>
    <string name="textview">TextView</string>
    <string name="button_label_hitung">Hitung</string>
    <string name="hitung_initial_value">0</string>
    <string name="toast_pesan">Hebat Bro!</string>
    <string name="button_main">Send</string>
    <string name="editText_main">Enter Your Message Here</string>
    <string name="text_header">Message Received</string>
    <string name="button_second">Reply</string>
    <string name="editText_second">Enter Your Reply Here</string>
    <string name="text_header_reply">Reply Received</string>
</resources>
```
## Output

![image](https://github.com/twn304/UTS_Mobile/assets/115573041/cfbcfff0-55ac-4302-9f7e-9200fea1fa97)
