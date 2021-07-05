# Clickable-ViewPager
Clickable ViewPager can help to add OnClick Functionaly in ViewPager in Android App.

## How to Add Clickable-ViewPager in Project
Add it in your root build.gradle at the end of repositories:
```Java
allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
```
Step 2. Add the dependency
```Java
dependencies {
	        implementation 'com.github.bdarvind:Clickable-ViewPager:1.0'
	}
```
## Implentation of Clickable-ViewPager in Activity
```java
public class MainActivity extends AppCompatActivity
        implements NavigationView.OnNavigationItemSelectedListener {


    ClickableViewPager mViewPager;
    //images array
    int[] images = {R.drawable.banner, R.drawable.banner2, R.drawable.banner3, R.drawable.banner4, R.drawable.banner5, R.drawable.banner, R.drawable.banner2, R.drawable.banner3, R.drawable.banner4, R.drawable.banner5};

    //Creating Object of ViewPagerAdapter
    ViewPagerAdapter mViewPagerAdapter;

    int currentPage = 0;
    Timer timer;
    final long DELAY_MS = 500;//delay in milliseconds before task is to be executed
    final long PERIOD_MS = 3000;
    int NUM_PAGES = 10;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toolbar toolbar = findViewById(R.id.toolbar);

        setSupportActionBar(toolbar);

        //Initializing the ViewPager Object
        mViewPager = (ClickableViewPager) findViewById(R.id.viewPapger);

        //Initializing the ViewPagerAdapter
        mViewPagerAdapter = new ViewPagerAdapter(MainActivity.this, images);

        //Adding the Adapter to the ViewPager
        mViewPager.setAdapter(mViewPagerAdapter);

        /*After setting the adapter use the timer */
        final Handler handler = new Handler();
        final Runnable Update = new Runnable() {
            public void run() {
                if (currentPage == NUM_PAGES-1) {
                    currentPage = 0;
                }
                mViewPager.setCurrentItem(currentPage++, true);
            }
        };

        timer = new Timer(); // This will create a new Thread
        timer.schedule(new TimerTask() { // task to be scheduled
            @Override
            public void run() {
                handler.post(Update);
            }
        }, DELAY_MS, PERIOD_MS);

        mViewPager.setOnItemClickListener(new ClickableViewPager.OnItemClickListener() {
            @Override
            public void onItemClick(int position) {
                // initializing object for custom chrome tabs.
                @Override
                    public void onClick(View v) {
                        // TODO Auto-generated method stub
                        Intent i = new Intent(getApplicationContext(),SecondActivity.class);
                        startActivity(i);
                    }

            }
        });
    }
}

```
