# 构建第一个Kotlin应用--生成随机数


## 创建一个新的工程
打开Android Studio，选择Projects>New Project，然后选择Basic Activity.

[图片]

点击Next，为应用程序命名（例如：My First App），选择Kotlin语言，然后点击Finish。Android Studio将使用系统中最新的API Level创建应用程序，并使用Gradle作为构建系统，在底部的视窗中可以查看整个过程。


## 创建模拟器
次步骤创建可以运行APP的模拟器，点击Tool>Device Manager或者工具栏上的按钮

[图片]

点击Create device，弹出创建模拟器的页面，

[图片]

选择想要创建模拟器设备（如Pixel 5），点击Next，在系统镜像页面的Recommended标签栏，选择最新镜像，

[图片]

然后首先下载镜像（Download），下载完成之后点击Next，完成模拟器命名和更多参数选择，最终点击Finish完成。注意：真实型号机型的模拟器镜像往往十分巨大，如果硬盘空间不足，考虑下载通用模拟器镜像。


## 在模拟器上运行应用程序
[图片]

## 向页面添加更多的布局
修改后的fragment_first.xml的代码

    <TextView
        android:id="@+id/textview_first"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="sans-serif-condensed"
        android:text="@string/hello_first_fragment"
        android:textColor="@android:color/white"
        android:textSize="72sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@id/random_button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.3" />

    <!--        app:layout_constraintVertical_bias="0.474" />-->

    <Button
        android:id="@+id/random_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="16dp"
        android:layout_marginBottom="88dp"
        android:background="@color/buttonBackground"
        android:text="@string/random_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <Button
        android:id="@+id/toast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginTop="220dp"
        android:background="@color/buttonBackground"
        android:text="@string/toast_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textview_first"
        app:layout_constraintVertical_bias="0.586" />

    <Button
        android:id="@+id/count_button"
        android:layout_width="152dp"
        android:layout_height="43dp"
        android:background="@color/buttonBackground"
        android:text="@string/Count"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/random_button"
        app:layout_constraintHorizontal_bias="0.536"
        app:layout_constraintStart_toEndOf="@+id/toast_button"
        app:layout_constraintTop_toBottomOf="@+id/textview_first"
        app:layout_constraintVertical_bias="0.798" />
    <!--        tools:layout_editor_absoluteY="494dp" />-->


## 添加代码完成应用程序交互

### TOAST按钮添加一个toast消息

打开FirstFragment.kt文件，有三个方法：onCreateView，onViewCreated和onDestroyView，在onViewCreated方法中使用绑定机制设置按钮的响应事件（创建应用程序时自带的按钮）。

        
		 binding.randomButton.setOnClickListener {
            val showCountTextView = view.findViewById<TextView>(R.id.textview_first)
            val currentCount = showCountTextView.text.toString().toInt()

            val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCount)

            findNavController().navigate(action)
            //findNavController().navigate(R.id.action_FirstFragment_to_SecondFragment)

         }
        // find the toast_button by its ID and set a click listener
        view.findViewById<Button>(R.id.toast_button).setOnClickListener {
            // create a Toast with some text, to appear for a short time
            val myToast = Toast.makeText(context, "Hello Toast!", Toast.LENGTH_LONG)
            // show the Toast
            myToast.show()
        }


