# Android-Studio1

new CountDownTimer(30000, 1000) {

    public void onTick(long millisUntilFinished) {
        mTextField.setText("seconds remaining: " + millisUntilFinished / 1000);
       //here you can have your logic to set text to edittext
    }

    public void onFinish() {
        mTextField.setText("done!");
    }

}.start();
-----------

new CountDownTimer(30000, 1000) {

    public void onTick(long millisUntilFinished) {
        mTextField.setText("seconds remaining: " + millisUntilFinished / 1000);
       //here you can have your logic to set text to edittext
    }

    public void onFinish() {
        mTextField.setText("done!");
    }

}.start();
------------
//Declare timer
CountDownTimer cTimer = null;

//start timer function
void startTimer() {
    cTimer = new CountDownTimer(30000, 1000) {
        public void onTick(long millisUntilFinished) {
        }
        public void onFinish() {
        }
    };
    cTimer.start();
}


//cancel timer
void cancelTimer() {
    if(cTimer!=null)
        cTimer.cancel();
}
-----------
package com.melikerdemkoc.countdown;

import android.os.Bundle;
import android.os.Handler;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.LinearLayout;
import android.widget.TextView;

import java.text.SimpleDateFormat;
import java.util.Date;

public class MainActivity extends AppCompatActivity {

    private String EVENT_DATE_TIME = "2020-12-31 10:30:00";
    private String DATE_FORMAT = "yyyy-MM-dd HH:mm:ss";
    private LinearLayout linear_layout_1, linear_layout_2;
    private TextView tv_days, tv_hour, tv_minute, tv_second;
    private Handler handler = new Handler();
    private Runnable runnable;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.count_down);

        initUI();
        countDownStart();
    }

    private void initUI() {
        linear_layout_1 = findViewById(R.id.linear_layout_1);
        linear_layout_2 = findViewById(R.id.linear_layout_2);
        tv_days = findViewById(R.id.tv_days);
        tv_hour = findViewById(R.id.tv_hour);
        tv_minute = findViewById(R.id.tv_minute);
        tv_second = findViewById(R.id.tv_second);
    }

    private void countDownStart() {
        runnable = new Runnable() {
            @Override
            public void run() {
                try {
                    handler.postDelayed(this, 1000);
                    SimpleDateFormat dateFormat = new SimpleDateFormat(DATE_FORMAT);
                    Date event_date = dateFormat.parse(EVENT_DATE_TIME);
                    Date current_date = new Date();
                    if (!current_date.after(event_date)) {
                        long diff = event_date.getTime() - current_date.getTime();
                        long Days = diff / (24 * 60 * 60 * 1000);
                        long Hours = diff / (60 * 60 * 1000) % 24;
                        long Minutes = diff / (60 * 1000) % 60;
                        long Seconds = diff / 1000 % 60;
                        //
                        tv_days.setText(String.format("%02d", Days));
                        tv_hour.setText(String.format("%02d", Hours));
                        tv_minute.setText(String.format("%02d", Minutes));
                        tv_second.setText(String.format("%02d", Seconds));
                    } else {
                        linear_layout_1.setVisibility(View.VISIBLE);
                        linear_layout_2.setVisibility(View.GONE);
                        handler.removeCallbacks(runnable);
                    }
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        };
        handler.postDelayed(runnable, 0);
    }

    protected void onStop() {
        super.onStop();
        handler.removeCallbacks(runnable);
    }
}
---------------
 <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/white"
    android:orientation="horizontal">

    <LinearLayout
        android:id="@+id/linear_layout_1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@android:color/black"
        android:gravity="center_horizontal"
        android:visibility="gone">

        <TextView
            android:id="@+id/tv_event"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_margin="20dp"
            android:text="Android Event Start"
            android:textColor="@android:color/white"
            android:textSize="20dp"
            android:textStyle="normal" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/linear_layout_2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@android:color/black"
        android:visibility="visible">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="vertical">

            <TextView
                android:id="@+id/tv_days"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="00"
                android:textColor="@android:color/white"
                android:textSize="20dp"
                android:textStyle="bold" />

            <TextView
                android:id="@+id/tv_days_title"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="Days"
                android:textColor="@android:color/white"
                android:textSize="20dp"
                android:textStyle="normal" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="vertical">

            <TextView
                android:id="@+id/tv_hour"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="00"
                android:textColor="@android:color/white"
                android:textSize="20dp"
                android:textStyle="bold" />

            <TextView
                android:id="@+id/tv_hour_title"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="Hour"
                android:textColor="@android:color/white"
                android:textSize="20dp"
                android:textStyle="normal" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="vertical">

            <TextView
                android:id="@+id/tv_minute"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="00"
                android:textColor="@android:color/white"
                android:textSize="20dp"
                android:textStyle="bold" />

            <TextView
                android:id="@+id/tv_minute_title"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="Minute"
                android:textColor="@android:color/white"
                android:textSize="20dp"
                android:textStyle="normal" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="vertical">

            <TextView
                android:id="@+id/tv_second"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="00"
                android:textColor="@android:color/white"
                android:textSize="20dp"
                android:textStyle="bold" />

            <TextView
                android:id="@+id/tv_second_title"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="Second"
                android:textColor="@android:color/white"
                android:textSize="20dp"
                android:textStyle="normal" />
        </LinearLayout>
    </LinearLayout>
</LinearLayout>
-------------------------
import java.util.concurrent.TimeUnit;
import android.app.Activity;
import android.os.Bundle;
import android.os.CountDownTimer;
import android.widget.TextView;


public class MainActivity extends Activity {


      TextView text1;

 private static final String FORMAT = "%02d:%02d:%02d";

 int seconds , minutes;

@Override
public void onCreate(Bundle savedInstanceState) {

    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);


    text1=(TextView)findViewById(R.id.textView1);

    new CountDownTimer(16069000, 1000) { // adjust the milli seconds here

        public void onTick(long millisUntilFinished) {

            text1.setText(""+String.format(FORMAT,
                    TimeUnit.MILLISECONDS.toHours(millisUntilFinished),
TimeUnit.MILLISECONDS.toMinutes(millisUntilFinished) - TimeUnit.HOURS.toMinutes(
                    TimeUnit.MILLISECONDS.toHours(millisUntilFinished)),
  TimeUnit.MILLISECONDS.toSeconds(millisUntilFinished) - TimeUnit.MINUTES.toSeconds(
                      TimeUnit.MILLISECONDS.toMinutes(millisUntilFinished))));              
        }

        public void onFinish() {
            text1.setText("done!");
        }
     }.start();             

  }

  }
  ----------------
   <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 android:orientation="vertical" >

<TextView
    android:id="@+id/textView1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_alignParentLeft="true"
    android:layout_alignParentTop="true"
    android:layout_marginLeft="34dp"
    android:layout_marginTop="58dp"
    android:text="Large Text"
    android:textAppearance="?android:attr/textAppearanceMedium" />

   </RelativeLayout>
   -----------------
   public void reverseTimer(int Seconds,final TextView tv){

    new CountDownTimer(Seconds* 1000+1000, 1000) {

        public void onTick(long millisUntilFinished) {
            int seconds = (int) (millisUntilFinished / 1000);
            int minutes = seconds / 60;
            seconds = seconds % 60;
            tv.setText("TIME : " + String.format("%02d", minutes)
                    + ":" + String.format("%02d", seconds));
        }

        public void onFinish() {
            tv.setText("Completed");
        }
    }.start();
}
---------------
public void reverseTimer(int Seconds, final TextView tv) {

    new CountDownTimer(Seconds * 1000 + 1000, 1000) {

        public void onTick(long millisUntilFinished) {
            int seconds = (int) (millisUntilFinished / 1000);

            int hours = seconds / (60 * 60);
            int tempMint = (seconds - (hours * 60 * 60));
            int minutes = tempMint / 60;
            seconds = tempMint - (minutes * 60);

            tv.setText("TIME : " + String.format("%02d", hours)
                    + ":" + String.format("%02d", minutes)
                    + ":" + String.format("%02d", seconds));
        }

        public void onFinish() {
            tv.setText("Completed");
        }
    }.start();
}
------------------

 Kotlin İle:

var timer = object: CountDownTimer(30000, 1000) {
        override fun onTick(millisUntilFinished: Long) {
            tvTimer.setText("seconds remaining: " + millisUntilFinished / 1000)
        }

        override fun onFinish() {
            tvTimer.setText("done!")
        }
    }
timer.start()
------------
