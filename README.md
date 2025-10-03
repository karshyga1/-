// структура 
HELLO,WORLD/SRC/JNI,OBJ,JNILIBS,JAVA,RES,ASSETS
структура JNI папки:
файлы:
android.mk
application.mk
main.cpp
папки:
substrate
KittyMemory
includes

//джава структура
Java/il2cpp
файлы:
ActivityMain.java
Main.java
Utils.java
папки
typefaces
//папка typefaces
typefaces:
CheckBox.java
ComponentBlock.java
Menu.java
PageButton.java
Slider.java

// java/il2cpp/typefaces файлы



Slider.java

package il2cpp.typefaces;
import android.content.Context;
import android.graphics.Color;
import android.graphics.PorterDuff;
import android.graphics.drawable.GradientDrawable;
import android.view.Gravity;
import android.widget.LinearLayout;
import android.widget.SeekBar;
import android.widget.SeekBar.OnSeekBarChangeListener;
import android.widget.TextView;
import il2cpp.Utils;
import android.graphics.Typeface;

// 1 line
public class Slider extends LinearLayout {
	Context context;
	public LinearLayout topLine, bottomLine;
	public TextView title, valueText;

	public SeekBar slider;

	public int max, current, value;
	public Callback callback;
	public int mainColor = 0;

	public static interface Callback {
		public void onChange(int value);
	}

	public void setCallback(Callback call) {
		callback = call;
	}

	public void setValue(int val, String name) {
		if (val > max) val = max;
		if (val < 0) val = 0;

		value = val;
		title.setText(name+" "+Integer.toString(value));
		slider.setProgress(value);
		if (callback != null) callback.onChange(value);
	}

	public Slider(Context ctx, final String name, int max1, int current1) {
		super(ctx);
		context = ctx;

		{ // Other
			max = max1;
			current = current1;
			value = current;
		}

		mainColor = Color.parseColor("#00ffff");
		setOrientation(LinearLayout.VERTICAL);

		bottomLine = new LinearLayout(context);
		{ //Bottom line (Decrease, Slider, Increase)
			bottomLine.setOrientation(LinearLayout.VERTICAL);
			bottomLine.setGravity(Gravity.CENTER);
			slider = new SeekBar(context);
			{ // Slider
			    slider.getThumb().mutate().setAlpha(0);
				slider.setBackgroundDrawable(null);
				GradientDrawable thumbr = new GradientDrawable();
				thumbr.setColor(Color.WHITE);
				thumbr.setCornerRadius(1);
				slider.setMax(max);
				slider.setProgress(current);
				GradientDrawable thumb = new GradientDrawable();
				thumb.setColor(mainColor);
				thumb.setSize(0,0);
				thumb.setCornerRadius(100);
				
				thumb.setTintMode(PorterDuff.Mode.MULTIPLY);

				slider.setThumb(thumb);

				slider.getProgressDrawable().setColorFilter(mainColor, PorterDuff.Mode.MULTIPLY);

				{
					slider.setOnSeekBarChangeListener(new OnSeekBarChangeListener() {
							@Override
							public void onProgressChanged(SeekBar sl, int v, boolean b) {
								setValue(v, name);
							}

							@Override
							public void onStopTrackingTouch(SeekBar sl) {}
							@Override
							public void onStartTrackingTouch(SeekBar sl) {}
						});
				}
			}


			bottomLine.setPadding(5, 0, 0, 0);

			title = new TextView(context);
			{ // Title slider
				title.setText(name+" "+Integer.toString(current));
				title.setTextSize(8f);
				title.setTypeface(Typeface.DEFAULT_BOLD);
				title.setTextColor(Color.WHITE);
				title.setGravity(Gravity.CENTER);
				//title.setPadding(0,5,0,5);
			}


		    bottomLine.addView(title, new LayoutParams(-1, -2));
			bottomLine.addView(slider, -1, -1);
			//bottomLine.addView(valueText, -1, -1);
		}
        GradientDrawable da = new GradientDrawable();
        da.setColor(-15592942);
        da.setCornerRadius(10f);
        setBackgroundDrawable(da);
		setPadding(5,0,5,10);
        LayoutParams lp = new LayoutParams(-1, Utils.dp(ctx,26));
        lp.bottomMargin = 5;
        setLayoutParams(lp);
		addView(bottomLine, -1,-1);
	}
}





PageButton.java

package il2cpp.typefaces;

import android.content.Context;
import android.graphics.Color;
import android.graphics.drawable.GradientDrawable;
import android.view.View;
import android.widget.ImageView;
import android.widget.LinearLayout;
import android.widget.TextView;
import il2cpp.Utils;

public class PageButton extends LinearLayout {
	Context context;
	
	public static interface Callback {
		public void onClick();
	}
	public Callback callback;
	View __isopen;
	
LinearLayout line;

ImageView icon;//делаем размер

	public void show() {
		__isopen.setVisibility(View.VISIBLE);
		
        
        {
            icon.setColorFilter(-8996237);

            GradientDrawable design = new GradientDrawable();
            design.setColor(-14737372);
            design.setCornerRadius(5f);
            design.setStroke(0, -13487809);
            icon.setBackgroundDrawable(design);
        }
        
        this.addView(line);
        
        
	}
	public int dpi(float dp) {
		float scale = context.getResources().getDisplayMetrics().density;
		return (int) (dp * scale + 0.5f);
	}
	
	public void hide() {
		__isopen.setVisibility(View.GONE);
        
        
		{
            icon.setColorFilter(-12237228);

        GradientDrawable design = new GradientDrawable();
            design.setColor(-15395047);
        design.setCornerRadius(5f);
        design.setStroke(0, -13487809);
        icon.setBackgroundDrawable(design);
        }
        
        this.removeView(line);
        
        }
	
	public void anim() {
		Utils.anim(this, 400);
	}
	
	public PageButton(Context context, String __src) {
		super(context);
		this.context = context;
		
		
		
				{
					this.setOrientation(LinearLayout.VERTICAL);
					this.setPadding(0,0,0,0);
					this.setGravity(17);
					
					GradientDrawable design = new GradientDrawable();
					design.setColor(0);
					design.setCornerRadii(new float[] { 0.0f, 0.0f, 0.0f, 0.0f, 0.0f, 0.0f, 0.0f, 0.0f });
					design.setStroke(0, -13487809);
					this.setBackgroundDrawable(design);
					
					LayoutParams lp = new LayoutParams(dpi(45), -1, 0);
					lp.leftMargin   = 0;
					lp.topMargin    = 0;
					lp.rightMargin  = 0;
					lp.bottomMargin = 0;
					this.setLayoutParams(lp);
				}
                
        
                icon = new ImageView(context);
               {
                   Utils.SetAssets(context, icon, "icon.png");
                   icon.setColorFilter(-12237228);
                   
                   GradientDrawable design = new GradientDrawable();
                   design.setColor(-15395047);
                   design.setCornerRadius(5f);
                   design.setStroke(0, -13487809);
                   icon.setBackgroundDrawable(design);

                   LayoutParams lp = new LayoutParams(-1, -1, 1);
                   lp.leftMargin   = 5;
                   lp.topMargin    = 0;
                   lp.rightMargin  = 5;
                   lp.bottomMargin = 10;
                   icon.setLayoutParams(lp);
               }
               this.addView(icon);
               
        line = new LinearLayout(context); 
        { 
            line.setOrientation(LinearLayout.VERTICAL); 
            line.setPadding(0,0,0,0); 
            line.setGravity(51); 
            
            GradientDrawable design = new GradientDrawable(); 
            design.setColor(-8996237); 
            design.setCornerRadius(5f); 
            design.setStroke(0, -16777216); 
            line.setBackgroundDrawable(design);
            
            LayoutParams lp = new LayoutParams(-1, dpi(2), 0); 
            lp.leftMargin   = 10; 
            lp.topMargin    = 0; 
            lp.rightMargin  = 10; 
            lp.bottomMargin = 0; 
            line.setLayoutParams(lp);
        } 
        
                
                
LinearLayout _isopen = new LinearLayout(context);

		__isopen = _isopen;
		
		this.setOnClickListener(new OnClickListener() {
			public void onClick(View v) {
				anim();
				if (callback != null) callback.onClick();
			}
		});
		Utils.SetAssets(context, icon, __src);
	}
}


Menu.java

package il2cpp.typefaces;

import android.app.Activity;
import android.content.Context;
import android.graphics.Color;
import android.graphics.PixelFormat;
import android.graphics.Typeface;
import android.graphics.drawable.GradientDrawable;
import android.os.Build;
import android.os.Handler;
import android.view.Gravity;
import android.view.MotionEvent;
import android.view.View;
import android.view.View.OnClickListener;
import android.view.WindowManager;
import android.widget.FrameLayout;
import android.widget.ImageView;
import android.widget.LinearLayout;
import android.widget.LinearLayout.LayoutParams;
import android.widget.ScrollView;
import android.widget.TextView;
import il2cpp.Utils;
import java.util.ArrayList;

class ColorList {
    public static int get_colorWhite() {
        return Color.parseColor("#91000000");
    }

    public static int get_colorLeft() {
        return Color.parseColor("#91000000");
    }

    public static int get_colorBlue() {
        return Color.parseColor("#91000000");
    }

    public static int get_colorBlack() {
        return Color.parseColor("#91000000");
    }

    public static int get_colorGray() {
        return Color.parseColor("#91000000");
    }

    public static int get_colorHeader() {
        return Color.parseColor("#91000000");
    }

    public static int colorMain () {
        return Color.parseColor("#101010");
    }

    public static int colorHeader () {
        return Color.parseColor("#9E000000");
    }

    public static int colorBody () {
        return Color.parseColor("#141414");
    }

    public static int colorGrayLight () {
        return Color.parseColor("#462c50");
    }

    public static int colorOrange () {
        return Color.parseColor("#CE04F2");
    }

    public static int colorRad() {
        return Color.parseColor("#ff0000");
    }
    public static int colorBLACKPON() {
        return Color.parseColor("#000000");
    }
    public static int colorBlue() {
        return Color.parseColor("#001aff"); 
    }
    public static int colorGreen() {
        return Color.parseColor("#04ff00"); 
    }

}

public class Menu
{




    protected int WIDTH,HEIGHT;

    public Typeface google(Context yes) {return Typeface.createFromAsset(yes.getAssets(), "Font.ttf");}


    protected Context context;
    protected FrameLayout _parentBox;
    ImageView _icon;
    protected ScrollView __scroll;
    protected LinearLayout __page;

    public ArrayList<LinearLayout> __pages = new ArrayList<>();
    
    boolean _isShow = false;

    public LinearLayout menulayout,l1,scrl,l2,pgs;
    public TextView text;

    
    public LinearLayout neon;

    protected WindowManager wmManager;
    protected WindowManager.LayoutParams wmParams;

    protected void init(Context context) {

        this.context = context;

        _parentBox = new FrameLayout(context);

        _parentBox.setOnTouchListener(handleMotionTouch);
        wmManager = ((Activity)context).getWindowManager();
        int aditionalFlags=0;
        if (Build.VERSION.SDK_INT >= 11)
            aditionalFlags = WindowManager.LayoutParams.FLAG_SPLIT_TOUCH;
        if (Build.VERSION.SDK_INT >=  3)
            aditionalFlags = aditionalFlags | WindowManager.LayoutParams.FLAG_ALT_FOCUSABLE_IM;
        wmParams = new WindowManager.LayoutParams(
            WindowManager.LayoutParams.WRAP_CONTENT,
            WindowManager.LayoutParams.WRAP_CONTENT,
            0,//initialX
            0,//initialy
            WindowManager.LayoutParams.TYPE_APPLICATION,
            WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE |
            WindowManager.LayoutParams.FLAG_LAYOUT_IN_OVERSCAN |
            WindowManager.LayoutParams.FLAG_LAYOUT_NO_LIMITS |
            WindowManager.LayoutParams.FLAG_FULLSCREEN |
            aditionalFlags,
            PixelFormat.TRANSPARENT
        );
        wmParams.gravity = Gravity.CENTER;//
    }

    public int dpi(float dp) {
        float scale = context.getResources().getDisplayMetrics().density;
        return (int) (dp * scale + 0.5f);
    }

    public void showMenu() {
        _isShow = true;
        _parentBox.removeAllViews();
        _parentBox.addView(menulayout);
    }

    public void hideMenu() {
        _isShow = false;
        new Handler().postDelayed(new Runnable() {
                public void run() {
                    _parentBox.removeAllViews();
                    _parentBox.addView(_icon, dpi(50),dpi(50));

                }
            }, 0);
    }
    
    
    
    
    



    public Menu(Context context)
    {
        init(context);

        _icon = new ImageView(context);
        {
            Utils.SetAssets(context,_icon,"icon.png");
        }

        menulayout = new LinearLayout(context);
        {
            menulayout.setOrientation(LinearLayout.VERTICAL);
            menulayout.setPadding(15,15,15,15);
            menulayout.setGravity(51);

            GradientDrawable design = new GradientDrawable();
            design.setColor(Color.parseColor("#000000"));
            design.setCornerRadius(10f);
            design.setStroke(0, -16777216);
            menulayout.setBackgroundDrawable(design);

            LayoutParams lp = new LayoutParams(dpi(450), dpi(350), 0);
            lp.leftMargin   = 0;
            lp.topMargin    = 0;
            lp.rightMargin  = 0;
            lp.bottomMargin = 0;
            menulayout.setLayoutParams(lp);
        }
        
        
        l1 = new LinearLayout(context);
        {
            l1.setOrientation(LinearLayout.HORIZONTAL);
            l1.setPadding(0,0,0,0);
            l1.setGravity(17);

            GradientDrawable design = new GradientDrawable();
            design.setColor(-15658735);
            design.setCornerRadius(10f);
            design.setStroke(0, -16777216);
            l1.setBackgroundDrawable(design);

            LayoutParams lp = new LayoutParams(-1, dpi(28), 0);
            lp.leftMargin   = 0;
            lp.topMargin    = 0;
            lp.rightMargin  = 0;
            lp.bottomMargin = 15;
            l1.setLayoutParams(lp);

        }
        menulayout.addView(l1);

        text = new TextView(context); 
        { 
            text.setText("FIXNEY | ImGui | Java"); 
            text.setTextColor(Color.parseColor("#00ffff")); 
            text.setShadowLayer(7,0,0,Color.parseColor("#00ffff"));
            text.setTextSize(13.0f); 
            text.setTypeface(Utils.font(context)); 
            text.setOnClickListener(new OnClickListener(){
                    @Override
                    public void onClick(View p1) {
                        hideMenu();
                    }});
        } 
        l1.addView(text);

        scrl = new LinearLayout(context);
        {
            scrl.setOrientation(LinearLayout.VERTICAL);
            scrl.setPadding(0,0,0,0);
            scrl.setGravity(51);

            GradientDrawable design = new GradientDrawable();
            design.setColor(0);
            design.setCornerRadius(10f);
            design.setStroke(0, -16777216);
            scrl.setBackgroundDrawable(design);

            LayoutParams lp = new LayoutParams(-1, -1, 1);
            lp.leftMargin   = 0;
            lp.topMargin    = 0;
            lp.rightMargin  = 0;
            lp.bottomMargin = 15;
            scrl.setLayoutParams(lp);
        }
        menulayout.addView(scrl);
        
        
        l2 = new LinearLayout(context);
        {
            l2.setOrientation(LinearLayout.HORIZONTAL);
            l2.setPadding(0,0,0,0);
            l2.setGravity(17);

            GradientDrawable design = new GradientDrawable();
            design.setColor(-15658735);
            design.setCornerRadius(10f);
            design.setStroke(0, -16777216);
            l2.setBackgroundDrawable(design);

            LayoutParams lp = new LayoutParams(-1, dpi(28), 0);
            lp.leftMargin   = 0;
            lp.topMargin    = 0;
            lp.rightMargin  = 0;
            lp.bottomMargin = 0;
            l2.setLayoutParams(lp);
        }
        menulayout.addView(l2);
        
        
        text = new TextView(context); 
        { 
            text.setText("t.me/Java_Source_F1XNEY"); 
            text.setTextColor(Color.parseColor("#00ffff")); 
            text.setShadowLayer(7,0,0,Color.parseColor("#00ffff"));
            text.setTextSize(13.0f); 
            text.setTypeface(Utils.font(context)); 
            text.setOnClickListener(new OnClickListener(){
                    @Override
                    public void onClick(View p1) {
                        hideMenu();
                    }});
        } 
        l2.addView(text);
        
        

        











        __scroll = new ScrollView(context);
        __scroll.setFillViewport(true);

        __page = new LinearLayout(context);
        __page.setOrientation(LinearLayout.VERTICAL);

        __scroll.addView(__page, -1, -1);
        scrl.addView(__scroll, -1, -1);

        __pages.add(__page);

        hideMenu();
       
        wmManager.addView(_parentBox, wmParams);
       
    }

    View.OnTouchListener handleMotionTouch = new View.OnTouchListener()
    {
        private float initX;          
        private float initY;
        private float touchX;
        private float touchY;

        double clock=0;

        @Override
        public boolean onTouch(View vw, MotionEvent ev)
        {

            switch (ev.getAction())
            {
                case MotionEvent.ACTION_DOWN:

                    initX = wmParams.x;
                    initY = wmParams.y;
                    touchX = ev.getRawX();
                    touchY = ev.getRawY();
                    clock = System.currentTimeMillis();
                    break;

                case MotionEvent.ACTION_MOVE:
                    wmParams.x = (int)initX + (int)(ev.getRawX() - touchX);

                    wmParams.y = (int)initY + (int)(ev.getRawY() - touchY);


                    wmManager.updateViewLayout(vw, wmParams);
                    break;

                case MotionEvent.ACTION_UP:
                    if (!_isShow && (System.currentTimeMillis() < (clock + 200)))
                    {
                        showMenu();
                    }
                    break;
            }
            return true;
        }
    };
}







ComponentBlock.java


package il2cpp.typefaces;
import android.content.Context;
import android.graphics.Color;
import android.graphics.drawable.GradientDrawable;
import android.view.Gravity;
import android.widget.LinearLayout;
import android.widget.ScrollView;
import android.widget.TextView;
import il2cpp.Utils;

public class ComponentBlock extends LinearLayout {
	Context context;
	
	public LinearLayout main,neon,header;
	public ScrollView scrl;
    public TextView title;
	
	public float corner = 1;
	public ComponentBlock(Context ctx, String name) {
		super(ctx);
		context = ctx;
		
        header = new LinearLayout(context);
        { // Header Layout
            GradientDrawable head = new GradientDrawable();
            head.setCornerRadius(10f);
            head.setColor(-15329511);
            header.setBackgroundDrawable(head);
            
            LayoutParams lp = new LayoutParams(-1, Utils.dp(context,18), 0);
            lp.leftMargin   = 0;
            lp.topMargin    = 0;
            lp.rightMargin  = 0;
            lp.bottomMargin = 8;
            header.setLayoutParams(lp);

            title = new TextView(context);
            { // Header title
                title.setText(name);
                title.setTextSize(9f);
                title.setTypeface(Utils.font(context));
                title.setTextColor(-1);
                title.setGravity(Gravity.CENTER);
                title.setPadding(0,0,0,0);
            }

            header.addView(title, new LayoutParams(-1, -1));
		}
        
		setOrientation(LinearLayout.VERTICAL);
		
		main = new LinearLayout(context);
		main.setOrientation(LinearLayout.VERTICAL);
		{ // Main content view
			GradientDrawable menu = new GradientDrawable();
			menu.setCornerRadius(10f);
			menu.setColor(-15658735);
			main.setBackgroundDrawable(menu
