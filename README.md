
# Ex.No:3 Design an android application Send SMS using Intent.


## AIM:

To create and design an android application Send SMS using Intent using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as smsintent and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Send SMS and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to create and design an android application Send SMS using Intent.
Developed by: Sanjit A
Registeration Number : 212224220087
*/
```

## MainActivity.java:
```
package com.example.muiex3;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.Manifest;
import android.content.pm.PackageManager;
import android.os.Bundle;
import android.telephony.SmsManager;
import android.util.Log;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity
{
    private static final String TAG = "MainActivity";
    private static final int REQUEST_SMS_PERMISSION = 100;

    EditText phoneNumberInput, messageInput;
    Button sendButton;

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        phoneNumberInput = findViewById(R.id.phone_number_input);
        messageInput = findViewById(R.id.message_input);
        sendButton = findViewById(R.id.send_button);

        sendButton.setOnClickListener(v -> checkAndSendSMS());
    }

    private void checkAndSendSMS()
    {
        String phoneNumber = phoneNumberInput.getText().toString();
        String message = messageInput.getText().toString();

        if (phoneNumber.isEmpty() || message.isEmpty())
        {
            Toast.makeText(this, "Please enter a phone number and a message.", Toast.LENGTH_SHORT).show();
            return;
        }

        if (ContextCompat.checkSelfPermission(this, Manifest.permission.SEND_SMS) != PackageManager.PERMISSION_GRANTED)
        {
            ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.SEND_SMS}, REQUEST_SMS_PERMISSION);
        }
        else
        {
            sendSMS(phoneNumber, message);
        }
    }

    private void sendSMS(String phoneNumber, String message)
    {
        try
        {
            SmsManager smsManager = getSystemService(SmsManager.class);
            if (smsManager != null) {
                smsManager.sendTextMessage(phoneNumber, null, message, null, null);
                Toast.makeText(this, "SMS sent successfully!", Toast.LENGTH_SHORT).show();
            } else {
                Toast.makeText(this, "Failed to get SmsManager.", Toast.LENGTH_SHORT).show();
            }
        }
        catch (Exception e)
        {
            Toast.makeText(this, "Failed to send SMS. Make sure permissions are granted.", Toast.LENGTH_LONG).show();
            Log.e(TAG, "Failed to send SMS", e);
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults)
    {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == REQUEST_SMS_PERMISSION)
        {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
            {
                String phoneNumber = phoneNumberInput.getText().toString();
                String message = messageInput.getText().toString();
                sendSMS(phoneNumber, message);
            }
            else
            {
                Toast.makeText(this, "SMS permission denied. Cannot send SMS.", Toast.LENGTH_SHORT).show();
            }
        }
    }
}

```

## activity_main.xml:
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp"
    android:gravity="center_horizontal"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:layout_marginBottom="32dp"
        android:text="@string/title_simple_sms_sender"
        android:textSize="24sp"
        android:textStyle="bold" />

    <EditText
        android:id="@+id/phone_number_input"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"
        android:autofillHints="phone"
        android:hint="@string/hint_phone_number"
        android:inputType="phone"
        android:minHeight="48dp"
        android:padding="12dp" />

    <EditText
        android:id="@+id/message_input"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="24dp"
        android:autofillHints="sms"
        android:gravity="top"
        android:hint="@string/hint_message"
        android:inputType="textMultiLine"
        android:minLines="3"
        android:padding="12dp" />

    <Button
        android:id="@+id/send_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:minHeight="48dp"
        android:text="@string/button_send_sms" />

</LinearLayout>

```

## AndroidManifist.xml:
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission
        android:name="android.permission.SEND_SMS"
        tools:ignore="ProtectedPermissions" />
    <uses-feature
        android:name="android.hardware.telephony"
        android:required="false" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MUIex3">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>

```

## OUTPUT

## MainActivity.java:
<img width="1917" height="1136" alt="image" src="https://github.com/user-attachments/assets/58835e93-1d5e-456a-92ab-bdf607a4bc74" />


## activity_main.xml:
<img width="1917" height="1131" alt="image" src="https://github.com/user-attachments/assets/c2a33aa5-6ad0-4f4e-b210-7835c07800f0" />


## AndroidManifist.xml:
<img width="1917" height="1140" alt="image" src="https://github.com/user-attachments/assets/5eed3bd8-d8ac-4e72-b4ce-b94d4d76afee" />


## SMS app:
<img width="1916" height="1137" alt="Screenshot 2026-11-04 084636" src="https://github.com/user-attachments/assets/25f194dc-8aef-44f0-9a30-731a77ed25b0" />

<img width="1915" height="1135" alt="Screenshot 2026-11-04 084709" src="https://github.com/user-attachments/assets/daae27aa-cf18-46b2-ba52-fa6ee9db0b20" />



## RESULT
Thus a Simple Android Application create and design an android application Send SMS using Intent using Android Studio is developed and executed successfully.
