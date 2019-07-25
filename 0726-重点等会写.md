
1. 修改了一个打卡bug

  ```
  /**
  
  - 人脸识别的时候需要 主动调取
    */
      public void handleParams() {
    Map<String, String> childParamsMap = tackCardChildParams();
    String error = mRequestBean.getError();
    if (!TextUtils.isEmpty(error) && mTackCardListener != null) {
        //清空一下error
        mRequestBean.setError("");
        mTackCardListener.onInnerError(error);
        return;
    }
    params = handleChildParamsMap(childParamsMap);
  
    //下面处理常规参数
    handleNormalParam(params, mRequestBean);
      }
  
    //通过这个方式进行了bug解决
    private void checkWifiAndGpsEmpty(TackCardRequestBean requestBean, String wifiId, String tackLocation) {
        boolean isWifi = TextUtils.isEmpty(wifiId);
        boolean isGps = TextUtils.isEmpty(tackLocation);
        if (isWifi && isGps) {
            requestBean.setError("正在获取定位，请稍后重试");
        }
    }
  ```

  

2.kotlin的静态代码块
	

```kotlin
    //静态代码块
    companion object {
        var INSTANCE: Context by Delegates.notNull()
    //静态代码块
    init {
        setDefaultRefreshHeaderCreator { context, layout ->
            layout.setPrimaryColorsId(R.color.colorPrimary, android.R.color.white)
            ClassicsHeader(context)
        }

        setDefaultRefreshFooterCreator { context, layout ->
            //指定为经典Footer，默认是 BallPulseFooter
            ClassicsFooter(context).setDrawableSize(20f)
        }
    }
}

相当于 java 中的
static {
	//写内容...
}
```

3.今天发现 fragment改版了
	在封装的时候，看到了 setUserVisibleHint 是个过期方法
	然后上面赫然的写到

	@Deprecated
	@link FragmentTransaction#setMaxLifecycle()
	
	 /**
	 * Set a hint to the system about whether this fragment's UI is currently visible
	 * to the user. This hint defaults to true and is persistent across fragment instance
	 * state save and restore.
	 *
	 * <p>An app may set this to false to indicate that the fragment's UI is
	 * scrolled out of visibility or is otherwise not directly visible to the user.
	 * This may be used by the system to prioritize operations such as fragment lifecycle updates
	 * or loader ordering behavior.</p>
	 *
	 * <p><strong>Note:</strong> This method may be called outside of the fragment lifecycle.
	 * and thus has no ordering guarantees with regard to fragment lifecycle method calls.</p>
	 *
	 * @param isVisibleToUser true if this fragment's UI is currently visible to the user (default),
	 *                        false if it is not.
	 *
	 * @deprecated Use {@link FragmentTransaction#setMaxLifecycle(Fragment, Lifecycle.State)}
	 * instead.
	 */
	@Deprecated
	public void setUserVisibleHint(boolean isVisibleToUser) {
	    if (!mUserVisibleHint && isVisibleToUser && mState < STARTED
	            && mFragmentManager != null && isAdded() && mIsCreated) {
	        mFragmentManager.performPendingDeferredStart(this);
	    }
	    mUserVisibleHint = isVisibleToUser;
	    mDeferStart = mState < STARTED && !isVisibleToUser;
	    if (mSavedFragmentState != null) {
	        // Ensure that if the user visible hint is set before the Fragment has
	        // restored its state that we don't lose the new value
	        mSavedUserVisibleHint = isVisibleToUser;
	    }
	}

   然后发现fragment 的 onResume 在 viewpager 中可以进行正常使用了

   发现 FragmentPagerAdapter 的构造方法多个参数，一个参数的也变成过期方法了

   public FragmentPagerAdapter(@NonNull FragmentManager fm,
            @Behavior int behavior) {
        mFragmentManager = fm;
        mBehavior = behavior;
    }

4. **自己记录更新，然后通过github记录每天在到底干了些什么，为什么没有别人优秀**

**是真的没什么时间，还是时间没有利用好**

5. 享学课堂，学到了 mvvm搭建一个新闻客户端

   




开源控件记录

轮廓界面 
https://github.com/OCNYang/ContourView

头部弹出toast（类似于qq的消息提示）
https://github.com/o0o0oo00/Pudding
到时可以参考这个做出任意的界面跳出吗？？？？


开源的一些汇总 
https://juejin.im/post/5b850b25f265da436f59052a





明天的计划

把  base 模块和 common模块， 通过 app的界面展示实验，

先完成 BaseFragment的抽取吧

通过借鉴上次fragment的那节课

