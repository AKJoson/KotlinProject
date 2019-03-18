## Kotlin 
* 定义变量可空

        var a : String?
        a = null
        a.length //也不会抛出NPE
        a!!.length //这样就会抛出NPE

## ViewModel

    class MainActivity : AppCompatActivity() {

    lateinit var binding: ActivityMainBinding

    var mainViewModel = MainViewModel()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
        binding.viewModel = mainViewModel
        binding.executePendingBindings()

    }
}

* 然而，我们旋转屏幕时候，一切会重新开始，所以～～数据丢失了。那么怎么破？我们可以让我们的ViewModel继承```android.arch.lifecycle.ViewModel```,这样我们可以使用：


class MainActivity : AppCompatActivity() {

    lateinit var binding: ActivityMainBinding
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
        //这样就可以拿到我们的ViewModel了，妈妈再也不用担心数据丢失了。
        binding.viewModel = ViewModelProviders.of(this).get(MainViewModel::class.java)
        binding.executePendingBindings()

    }
}
