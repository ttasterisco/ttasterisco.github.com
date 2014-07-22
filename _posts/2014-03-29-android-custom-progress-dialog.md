---
layout: post
title: Customizing Android's Progress Dialog
summary: Make Android Less Boring.
---

Hey! If you're reading this, it means that, just like me, you've done some Android app that does some kind of time consuming operation like a network request or getting stuff from the database and so on, right?
And, <i>obviously</i>, you did that in an `AsyncTask`. And because you don't really have anything to show the user and don't want them poking around, you forced a `ProgressDialog` onto them.

But were you using the out of the box `ProgressDialog` like this?

<img src="/resources/2014-03-29-android-custom-progress-dialog/plain-old-progress-dialog.png" width="240" height="427">

Kind of boring, don't you think? I mean, it works fine, but what if we could spice the app a little bit, entertain ours users and all in 5 minutes' work?
That sounds great, doesn't it? Well, we can!

What I'm about to show you is something very simple! Just have our own animation going around while our time-consuming-operation happens!
Like this:

<img src="/resources/2014-03-29-android-custom-progress-dialog/custom-progress-dialog-in-action.gif" width="240" height="427">

So here's how to do it:

Customizing the Progress Dialog means nothing more than extending `ProgressDialog` and setting our own layout!
Yes, that means we can virtually do anything in there! But lets not go too crazy, ok?

<pre>
<code>
  public class MyCustomProgressDialog extends ProgressDialog {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.view_custom_progress_dialog);

      ...
    }

    ...
  }
</code>
</pre>

The `CustomProgressDialog`'s layout is nothing more than a container with an `Imageview`! Pretty simple.

    <LinearLayout
      xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:gravity="center"
      android:background="@null"
    >
      <ImageView
        android:id="@+id/animation"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:contentDescription="@string/empty_string"
        android:scaleType="centerCrop"
        android:adjustViewBounds="true"
      />
    </LinearLayout>


But how do we make this move? Well, we can use a [Drawable Animation](http://developer.android.com/guide/topics/graphics/drawable-animation.html)! We start by creating an `AnimationDrawable` - it's just a file where you define a sequence of images in the order you want them to appear and for how long each should appear. Sounds familiar? Yes, that's how exactly GIFs work! And you can say if you want it to loop or not! (Yes, that means you'll need to create a few images for your animation - or you could just extract the frames from some funny GIF from the interwebs!).

  <?xml version="1.0" encoding="utf-8"?>
  <animation-list xmlns:android="http://schemas.android.com/apk/res/android" android:oneshot="false">
    <item android:drawable="@drawable/anim00" android:duration="250" />
    <item android:drawable="@drawable/anim01" android:duration="250" />
    <item android:drawable="@drawable/anim02" android:duration="250" />
    <item android:drawable="@drawable/anim03" android:duration="250" />
  </animation-list>

Once we have our animation list ready, we just need to use it in our layout. Remember the `ImageView` in the `CustomProgressDialog`'s layout? We just need to bind the things together!

We define an `AnimationDrawable`

    public class MyCustomProgressDialog extends ProgressDialog {
      private AnimationDrawable animation;

      ...
    }

and we can bind it `onCreate`

    @Override
    protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.view_custom_progress_dialog);

      ImageView la = (ImageView) findViewById(R.id.animation);
      la.setBackgroundResource(R.drawable.custom_progress_dialog_animation);
      animation = (AnimationDrawable) la.getBackground();
    }

then we can complete our `ProgressDialog` by overriding `show` and `dismiss`

    @Override
    public void show() {
      super.show();
      animation.start();
    }

    @Override
    public void dismiss() {
      super.dismiss();
      animation.stop();
    }

And <b>I</b> like to use a static constructor for the `ProgressDialog`

    public static ProgressDialog ctor(Context context) {
      MyCustomProgressDialog dialog = new MyCustomProgressDialog(context);
      dialog.setIndeterminate(true);
      dialog.setCancelable(false);
      return dialog;
    }

That's the core of it! Now, in our `AsyncTask`, we can create and call our `CustomProgressDialog` and have it show our awesome animation!

    class VeryLongAsyncTask extends AsyncTask<Void, Void, Void> {
      private final ProgressDialog progressDialog;

      public VeryLongAsyncTask(Context ctx) {
        progressDialog = MyCustomProgressDialog.ctor(ctx);
      }

      @Override
      protected void onPreExecute() {
        super.onPreExecute();
        textView.setVisibility(View.INVISIBLE);

        progressDialog.show();
      }

      @Override
      protected Void doInBackground(Void... params) {
        // sleep for 5 seconds
        try { Thread.sleep(5000); }
        catch (InterruptedException e) { e.printStackTrace(); }

        return null;
      }

      @Override
      protected void onPostExecute(Void result) {
        super.onPostExecute(result);
        textView.setVisibility(View.VISIBLE);

        progressDialog.hide();
      }
    }

And that's it! Simple and easily reusable in our future apps! Here's an [example project](https://github.com/ttasterisco/CustomProgressDialogExample) that you can test.
Enjoy!

Conception date: March 25th, 2014
