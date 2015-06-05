# MakeAndroidSpeakforYOU
**An Application that converts texts into voice.**  

Android allows you convert your text into voice.  
Not only you can convert it but it also allows you to speak text in variety of different languages.  

So there is built in sdk TextToSpeech class for this purpose. In order to use this class,  
you need to instantiate an object of this class and also specify the initListner. Its syntax is given below:  

**Android provides TextToSpeech class for this purpose. In order to use this  
class, you need to instantiate an object of this class and also specify the initListner. Its syntax is given below:**

```sh

private EditText write;
ttobj=new TextToSpeech(getApplicationContext(), 
new TextToSpeech.OnInitListener() { 
          @Override public void onInit(int status) {
          } 
          } );

```

in the above listner you can specify the properties for TextToSpeech object ,  
such as its language ,pitch e.t.c. Language can be set by calling setLanguage() method. Its syntax is given below:

```sh
-----------------------------
ttobj.setLanguage(Locale.UK);
-----------------------------
Sr.No | Locale
1     |   US 
2     |   CANADA_FRENCH 
3     |   GERMANY 
4     |   ITALY
5     |   JAPAN 
6     |   CHINA

```
  
you can call speak method of the class to speak the text. Its syntax is given below: 
```sh
ttobj.speak(toSpeak, TextToSpeech.QUEUE_FLUSH, null);
```

![Screen](https://github.com/ashokslsk/MakeAndroidSpeakforYOU/blob/master/screens/main.png)
![Screen](https://github.com/ashokslsk/MakeAndroidSpeakforYOU/blob/master/screens/second.png)

You can use my java and xml classes for your easy implementation.... :) 

MainActivity.java

```sh
package your_package_identifier;
import android.app.Activity;
import android.os.Bundle;
import android.speech.tts.TextToSpeech;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.EditText;

import com.gitonway.lee.niftymodaldialogeffects.lib.Effectstype;
import com.gitonway.lee.niftymodaldialogeffects.lib.NiftyDialogBuilder;

import java.util.Locale;

public class MainActivity extends Activity {
    TextToSpeech ttobj;
    private EditText write;
    NiftyDialogBuilder dialogBuilder;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        write = (EditText) findViewById(R.id.editText1);
        ttobj = new TextToSpeech(getApplicationContext(),
                new TextToSpeech.OnInitListener() {
                    @Override
                    public void onInit(int status) {
                        if (status != TextToSpeech.ERROR) {
                            ttobj.setLanguage(Locale.UK);
                        }
                    }
                });
    }

    @Override
    public void onPause() {
        if (ttobj != null) {
            ttobj.stop();
            ttobj.shutdown();
        }
        super.onPause();
    }

    public void speakText(View view) {
        String toSpeak = write.getText().toString();
      // You can use Simple Toast if you can't use the NiftyDialogBuilder  
      
        dialogBuilder = NiftyDialogBuilder.getInstance(MainActivity.this);
        dialogBuilder
                .withTitle("The text entered is rendering....!")
                .withTitleColor("#FFFFFF")
                .withDividerColor("#11000000")
                .withMessage(toSpeak)
                        //.withTitle(null)  no title
                .withTitleColor("#FFFFFF")                                  //def
                .withDividerColor("#11000000")                              //def
                .withMessageColor("#FFFFFFFF")                              //def  | withMessageColor(int resid)
                .withDialogColor("#2980b9")
                .withDuration(700)                                          //def
                .withEffect(Effectstype.Fliph)
                .show();

       // Toast.makeText(getApplicationContext(), toSpeak, Toast.LENGTH_SHORT).show();
        ttobj.speak(toSpeak, TextToSpeech.QUEUE_FLUSH, null);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.menu_main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_settings) {
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
}


```  
activity_main.xml
```sh
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context=".MainActivity">

    <com.gc.materialdesign.views.ButtonRectangle
        android:id="@+id/button1"
        android:layout_width="120dp"
        android:layout_height="80dp"
        android:layout_centerHorizontal="true"
        android:layout_below="@+id/editText1"
        android:background="#1E88E5"
        android:onClick="speakText"
        android:text="@string/text1"
        android:textColor="#fff" />

    <EditText
        android:id="@+id/editText1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/textView1"
        android:layout_centerHorizontal="true"
        android:ems="10">

        <requestFocus />
    </EditText>

    <TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="82dp"
        android:text="@string/write"
        android:textAppearance="?android:attr/textAppearanceLarge" />

</RelativeLayout>
```  
  
  
Finally your done now.

- Execute it as simple as it is 

* [For more codes, funs and for queries be in touch with @ashokslsk ](https://github.com/ashokslsk)





