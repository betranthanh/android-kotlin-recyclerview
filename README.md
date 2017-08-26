## Android Kotlin RecyclerView
### 1. Add RecyclerView
```java
var recyclerView: RecyclerView? = null
recyclerView = findViewById(R.id.recyclerView)
```

### 2. Create your model
```java
class UserDto {
    var name: String = ""
    var comment: String = ""

    constructor() {}

    constructor(name: String, comment: String) {
        this.name = name
        this.comment = comment
    }
}
```
### 3. Create row layout
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">

    <ImageView
        android:id="@+id/imgAvatar"
        android:layout_width="60dp"
        android:layout_height="60dp"
        android:layout_margin="10dp"
        android:src="@drawable/avatar1" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_centerVertical="true"
        android:layout_toRightOf="@id/imgAvatar"
        android:orientation="vertical">

        <TextView
            android:id="@+id/txtName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Name"
            android:textStyle="bold"
            />
        <TextView
            android:id="@+id/txtComment"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="comment"/>
    </LinearLayout>
</RelativeLayout>
```
### 4. Create adapter class
```java
class UsersAdapter(private var items: ArrayList<UserDto>): RecyclerView.Adapter<UsersAdapter.ViewHolder>() {

    override fun getItemCount(): Int {
        return items.size
    }

    override fun onBindViewHolder(holder: ViewHolder?, position: Int) {
        var userDto = items[position]
        holder?.txtName?.text = userDto.name
        holder?.txtComment?.text = userDto.comment
    }

    override fun onCreateViewHolder(parent: ViewGroup?, viewType: Int): ViewHolder {
        val itemView = LayoutInflater.from(parent?.context)
                .inflate(R.layout.user_list_row, parent, false)

        return ViewHolder(itemView)
    }

    class ViewHolder(row: View) : RecyclerView.ViewHolder(row) {
        var txtName: TextView? = null
        var txtComment: TextView? = null

        init {
            this.txtName = row?.findViewById<TextView>(R.id.txtName)
            this.txtComment = row?.findViewById<TextView>(R.id.txtComment)
        }
    }
}
```

### 5. Combine all together
```java
var adapter = UsersAdapter(generateData())
val layoutManager = LinearLayoutManager(applicationContext)
recyclerView?.layoutManager = layoutManager
recyclerView?.itemAnimator = DefaultItemAnimator()

recyclerView?.adapter = adapter
adapter.notifyDataSetChanged()
....
fun generateData(): ArrayList<UserDto> {
    var result = ArrayList<UserDto>()

    for (i in 0..9) {
        var user: UserDto = UserDto("Bett", "Awesome work ;)")
        result.add(user)
    }

    return result
}
```

## Video follow above steps
[![Watch the video](http://i.imgur.com/QBxc8b3l.png)](https://goo.gl/9ipBif)

## Contact
Drop me an email if you want discuss anything further. [Email](betranthanh@gmail.com)

## License
Licensed under the MIT license.
