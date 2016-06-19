# AndSes4Ass2
Main Activity.java
package me.rk.andses4ass2;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {
    Button customListView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        customListView=(Button) findViewById(R.id.customListView);
        customListView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent=new Intent(MainActivity.this, CustomListview.class);
                startActivity(intent);
            }
        });
    }
}


CustomListView.java
package me.rk.andses4ass2;

import android.app.Activity;
import android.os.Bundle;
import android.widget.ListView;
import android.widget.AdapterView;
import android.widget.ListAdapter;

/**
 * Created by airodyra on 6/19/2016.
 */
public class CustomListview extends Activity{

    ListView listView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.second_activity);

        listView=(ListView)findViewById(R.id.listView);

        final String[] nameArray={"Name1", "Name2", "Name3", "Name4", "Name5", "Name6", "Name7"};
        final String[] phoneArray={"PhoneNumber1", "PhoneNumber2", "PhoneNumber3", "PhoneNumber4",
                "PhoneNumber5", "PhoneNumber6", "PhoneNumber7"};

        CustomAdaptor customAdaptor=new CustomAdaptor(CustomListview.this, nameArray, phoneArray);
        listView.setAdapter(customAdaptor);


    }
}


CustomAdaptor.java
package me.rk.andses4ass2;

import android.content.Context;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.TextView;

/**
 * Created by airodyra on 6/19/2016.
 */
public class CustomAdaptor extends BaseAdapter{

    private Context mContext;
    private String[] mName;
    private String[] mphone;

    public CustomAdaptor (Context context, String[]name, String[]phone){
        mContext=context;
        mName=name;
        mphone=phone;;
    }
    @Override
    public int getCount() {
        return mName.length;
    }

    @Override
    public Object getItem(int position) {
        return position;
    }

    @Override
    public long getItemId(int position) {
        return position;
    }
    public class ViewHolder{
        TextView nameTextView;
        TextView phonenumberTextView;

    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder viewHolder;

        if(convertView==null){
            viewHolder=new ViewHolder();
            View rootView=View.inflate(mContext, R.layout.custom_list_view,null);
            viewHolder.nameTextView=(TextView) rootView.findViewById(R.id.name);
            viewHolder.phonenumberTextView=(TextView) rootView.findViewById(R.id.phone);

            rootView.setTag(viewHolder);
            convertView=rootView;
        }
        else {
            viewHolder=(ViewHolder) convertView.getTag();
        }

        viewHolder.nameTextView.setText(mName[position]);
        viewHolder.phonenumberTextView.setText((mphone[position]));
        return convertView;
    }
}

Activity Main.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="me.rk.andses4ass2.MainActivity">

    <Button
        android:id="@+id/customListView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="21dp"
        android:text="Custom ListView"
        android:layout_centerHorizontal="true"/>
</RelativeLayout>


Second Activity.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"></ListView>
</LinearLayout>

Custom_List_View.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@android:color/holo_blue_dark"
    android:padding="10dp">

    <TextView
        android:id="@+id/name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Name1"
        android:textSize="20dp" />

    <TextView
        android:id="@+id/phone"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="PhoneNumber1"
        android:textSize="20dp" />
</LinearLayout>
